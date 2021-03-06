---
title: FTPFactory
author: PipisCrew
date: 2017-03-24
categories: [.net]
toc: true
---

```js
    /* 
    FTPFactory.cs @ 2004
    Better view with tab space=4 

    Written by Jaimon Mathew (jaimonmathew@rediffmail.com) 
    Rolander,Dan (Dan.Rolander@marriott.com) has modified the download 
    method to cope with file name with path information. He also 
    provided the XML comments so that the library provides Intellisense 
    descriptions. 
    */

    using System;
    using System.Net;
    using System.IO;
    using System.Text;
    using System.Net.Sockets;

    namespace Common
    {
        ///

        /// This class provides the functionality for FTP Server connection 
        /// and related functions. 
        ///

        public class FTPFactory
        {
            private string remoteHost, remotePath, remoteUser, remotePass, mes;
            private int remotePort, bytes;
            private Socket clientSocket;

            private int retValue;
            private Boolean debug;
            private Boolean logined;
            private string reply;

            private static int BLOCK_SIZE = 512;

            Byte[] buffer = new Byte[BLOCK_SIZE];
            Encoding ASCII = Encoding.ASCII;

            ///

            /// Default constuctor for FTP Factory class 
            ///

            public FTPFactory()
            {
                remoteHost = "localhost";
                remotePath = ".";
                remoteUser = null;
                remotePass = null;
                remotePort = 21;
                debug = false;
                logined = false;
            }

            ///

            /// Sets the name of the FTP server to connect to 
            ///

            /// Remote host Name 
            public void setRemoteHost(string remoteHost)
            {
                this.remoteHost = remoteHost;
            }

            ///

            /// Returns the name of the current FTP server 
            ///

            /// Host Name 
            public string getRemoteHost()
            {
                return remoteHost;
            }

            ///

            /// Sets the port number to use for FTP. 
            ///

            /// Port number 
            public void setRemotePort(int remotePort)
            {
                this.remotePort = remotePort;
            }

            ///

            /// Returns the current port number. 
            ///

            /// Current port number 
            public int getRemotePort()
            {
                return remotePort;
            }

            ///

            /// Sets the remote directory path. 
            ///

            /// The remote directory path 
            public void setRemotePath(string remotePath)
            {
                this.remotePath = remotePath;
            }

            ///

            /// Return the current remote directory path. 
            ///

            /// The current remote directory path. 
            public string getRemotePath()
            {
                return remotePath;
            }

            ///

            /// Sets the user name to use for logging into the remote server. 
            ///

            /// Username 
            public void setRemoteUser(string remoteUser)
            {
                this.remoteUser = remoteUser;
            }

            ///

            /// Sets the password to user for logging into the remote server. 
            ///

            /// Password 
            public void setRemotePass(string remotePass)
            {
                this.remotePass = remotePass;
            }

            ///

            /// Returns a string array containing the remote directory's file list. 
            ///

            /// Mask to be used for filteration 
            /// List of files in string array format 
            public string[] getFileList(string mask)
            {
                if (!logined)
                {
                    login();
                }

                Socket cSocket = createDataSocket();

                sendCommand("NLST " + mask);

                if (!(retValue == 150 || retValue == 125))
                {
                    throw new IOException(reply.Substring(4));
                }

                mes = "";

                while (true)
                {
                    int bytes = cSocket.Receive(buffer, buffer.Length, 0);
                    mes += ASCII.GetString(buffer, 0, bytes);

                    if (bytes < buffer.Length)
                    {
                        break;
                    }
                }

                char[] seperator = { '\n' };
                string[] mess = mes.Split(seperator);

                cSocket.Close();

                readReply();

                if (retValue != 226)
                {
                    throw new IOException(reply.Substring(4));
                }
                return mess;
            }

            ///

            /// Returns the size of a file. 
            ///

            /// Name of the file for which the size is required 
            /// size in long format 
            public long getFileSize(string fileName)
            {
                if (!logined)
                {
                    login();
                }

                sendCommand("SIZE " + fileName);
                long size = 0;

                if (retValue == 213)
                {
                    size = Int64.Parse(reply.Substring(4));
                }
                else
                {
                    throw new IOException(reply.Substring(4));
                }

                return size;
            }

            ///

            /// Login to the remote server. 
            ///

            public void login()
            {
                clientSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                IPEndPoint ep = new IPEndPoint(Dns.Resolve(remoteHost).AddressList[0], remotePort);

                try
                {
                    clientSocket.Connect(ep);
                }
                catch (Exception)
                {
                    throw new IOException("Couldn't connect to remote server");
                }

                readReply();
                if (retValue != 220)
                {
                    close();
                    throw new IOException(reply.Substring(4));
                }
                if (debug)
                    Console.WriteLine("USER " + remoteUser);

                sendCommand("USER " + remoteUser);

                if (!(retValue == 331 || retValue == 230))
                {
                    cleanup();
                    throw new IOException(reply.Substring(4));
                }

                if (retValue != 230)
                {
                    if (debug)
                        Console.WriteLine("PASS xxx");

                    sendCommand("PASS " + remotePass);
                    if (!(retValue == 230 || retValue == 202))
                    {
                        cleanup();
                        throw new IOException(reply.Substring(4));
                    }
                }

                logined = true;
                Console.WriteLine("Connected to " + remoteHost);

                chdir(remotePath);
            }

            ///

            /// Sets the mode for file transfer 
            ///

            /// Value of the Mode, if the value of mode is true, set binary mode for downloads, else set Ascii mode. 
            public void setBinaryMode(Boolean mode)
            {
                if (mode)
                {
                    sendCommand("TYPE I");
                }
                else
                {
                    sendCommand("TYPE A");
                }
                if (retValue != 200)
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Download a file to the Assembly's local directory, keeping the same file name. 
            ///

            /// File to be downlaoded 
            public void download(string remFileName)
            {
                download(remFileName, "", false);
            }

            ///

            /// Download a remote file to the Assembly's local directory, 
            /// keeping the same file name, and set the resume flag. 
            ///

            /// File to be downlaoded 
            /// Flag to set if the resume is managed or not 
            public void download(string remFileName, Boolean resume)
            {
                download(remFileName, "", resume);
            }

            ///

            /// Download a remote file to a local file name which can include 
            /// a path. The local file name will be created or overwritten, 
            /// but the path must exist. 
            ///

            /// File to be downlaoded 
            /// Local file name 
            public void download(string remFileName, string locFileName)
            {
                download(remFileName, locFileName, false);
            }

            ///

            /// Download a remote file to a local file name which can include 
            /// a path, and set the resume flag. The local file name will be 
            /// created or overwritten, but the path must exist. 
            ///

            /// File to be downlaoded 
            /// Local file name 
            /// Flag stating if it is required to set the resume 
            public void download(string remFileName, string locFileName, Boolean resume)
            {
                if (!logined)
                {
                    login();
                }

                setBinaryMode(true);

                Console.WriteLine("Downloading file " + remFileName + " from " + remoteHost + "/" + remotePath);

                if (locFileName.Equals(""))
                {
                    locFileName = remFileName;
                }

                if (!File.Exists(locFileName))
                {
                    Stream st = File.Create(locFileName);
                    st.Close();
                }

                FileStream output = new FileStream(locFileName, FileMode.Open);

                Socket cSocket = createDataSocket();

                long offset = 0;

                if (resume)
                {

                    offset = output.Length;

                    if (offset > 0)
                    {
                        sendCommand("REST " + offset);
                        if (retValue != 350)
                        {
                            //throw new IOException(reply.Substring(4)); 
                            //Some servers may not support resuming. 
                            offset = 0;
                        }
                    }

                    if (offset > 0)
                    {
                        if (debug)
                        {
                            Console.WriteLine("seeking to " + offset);
                        }
                        long npos = output.Seek(offset, SeekOrigin.Begin);
                        Console.WriteLine("new pos=" + npos);
                    }
                }

                sendCommand("RETR " + remFileName);

                if (!(retValue == 150 || retValue == 125))
                {
                    throw new IOException(reply.Substring(4));
                }

                while (true)
                {
                    bytes = cSocket.Receive(buffer, buffer.Length, 0);
                    output.Write(buffer, 0, bytes);

                    if (bytes <= 0)
                    {
                        break;
                    }
                }

                output.Close();
                if (cSocket.Connected)
                {
                    cSocket.Close();
                }

                Console.WriteLine("");

                readReply();

                if (!(retValue == 226 || retValue == 250))
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Uploads a file 
            ///

            /// File name to be uplaoded 
            public void upload(string fileName)
            {
                upload(fileName, false);
            }

            ///

            /// Upload a file and set the resume flag. 
            ///

            /// File name to be uplaoded 
            /// Flag to set if the operation needs the resume functionality 
            public void upload(string fileName, Boolean resume)
            {
                if (!logined)
                {
                    login();
                }

                Socket cSocket = createDataSocket();
                long offset = 0;

                if (resume)
                {
                    try
                    {
                        setBinaryMode(true);
                        offset = getFileSize(fileName);
                    }
                    catch (Exception)
                    {
                        offset = 0;
                    }
                }

                if (offset > 0)
                {
                    sendCommand("REST " + offset);
                    if (retValue != 350)
                    {
                        //throw new IOException(reply.Substring(4)); 
                        //Remote server may not support resuming. 
                        offset = 0;
                    }
                }

                sendCommand("STOR " + Path.GetFileName(fileName));

                if (!(retValue == 125 || retValue == 150))
                {
                    throw new IOException(reply.Substring(4));
                }

                // open input stream to read source file 
                FileStream input = new FileStream(fileName, FileMode.Open);

                if (offset != 0)
                {
                    if (debug)
                    {
                        Console.WriteLine("seeking to " + offset);
                    }
                    input.Seek(offset, SeekOrigin.Begin);
                }

                Console.WriteLine("Uploading file " + fileName + " to " + remotePath);

                while ((bytes = input.Read(buffer, 0, buffer.Length)) > 0)
                {
                    cSocket.Send(buffer, bytes, 0);
                }
                input.Close();

                Console.WriteLine("");

                if (cSocket.Connected)
                {
                    cSocket.Close();
                }

                readReply();
                if (!(retValue == 226 || retValue == 250))
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Deletes a file from the remote FTP server. 
            ///

            /// File name to be deleted 
            public void deleteRemoteFile(string fileName)
            {

                if (!logined)
                {
                    login();
                }

                sendCommand("DELE " + fileName);

                if (retValue != 250)
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Renames a file on the remote FTP server. 
            ///

            /// Old File Name 
            /// New File Name 
            public void renameRemoteFile(string oldFileName, string newFileName)
            {
                if (!logined)
                {
                    login();
                }

                sendCommand("RNFR " + oldFileName);

                if (retValue != 350)
                {
                    throw new IOException(reply.Substring(4));
                }

                // known problem 
                // rnto will not take care of existing file. 
                // i.e. It will overwrite if newFileName exist 
                sendCommand("RNTO " + newFileName);
                if (retValue != 250)
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Creates a directory on the remote FTP server. 
            ///

            /// Name of the directory 
            public void mkdir(string dirName)
            {
                if (!logined)
                {
                    login();
                }

                sendCommand("MKD " + dirName);

                if (retValue != 250)
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Deletes a directory on the remote FTP server. 
            ///

            /// Removes the directory 
            public void rmdir(string dirName)
            {
                if (!logined)
                {
                    login();
                }

                sendCommand("RMD " + dirName);

                if (retValue != 250)
                {
                    throw new IOException(reply.Substring(4));
                }
            }

            ///

            /// Change the current working directory on the remote FTP server. 
            ///

            /// New directory Name 
            public void chdir(string dirName)
            {
                if (dirName.Equals("."))
                {
                    return;
                }

                if (!logined)
                {
                    login();
                }

                sendCommand("CWD " + dirName);

                if (retValue != 250)
                {
                    throw new IOException(reply.Substring(4));
                }

                this.remotePath = dirName;

                Console.WriteLine("Current directory is " + remotePath);
            }

            ///

            /// Close the FTP connection. 
            ///

            public void close()
            {
                if (clientSocket != null)
                {
                    sendCommand("QUIT");
                }
                cleanup();
                Console.WriteLine("Closing...");
            }

            ///

            /// Set debug mode. 
            ///

            /// 
            public void setDebug(Boolean debug)
            {
                this.debug = debug;
            }

            // Reads a reply from the server 
            private void readReply()
            {
                mes = "";
                reply = readLine();
                retValue = Int32.Parse(reply.Substring(0, 3));
            }

            // Clean up the socket connections 
            private void cleanup()
            {
                if (clientSocket != null)
                {
                    clientSocket.Close();
                    clientSocket = null;
                }
                logined = false;
            }

            // Read line 
            private string readLine()
            {
                while (true)
                {
                    bytes = clientSocket.Receive(buffer, buffer.Length, 0);
                    mes += ASCII.GetString(buffer, 0, bytes);
                    if (bytes < buffer.Length)
                    {
                        break;
                    }
                }

                char[] seperator = { '\n' };
                string[] mess = mes.Split(seperator);

                if (mes.Length > 2)
                {
                    mes = mess[mess.Length - 2];
                }
                else
                {
                    mes = mess[0];
                }

                if (!mes.Substring(3, 1).Equals(" "))
                {
                    return readLine();
                }

                if (debug)
                {
                    for (int k = 0; k < mess.Length - 1; k++)
                    {
                        Console.WriteLine(mess[k]);
                    }
                }
                return mes;
            }

            private void sendCommand(String command)
            {
                Byte[] cmdBytes = Encoding.ASCII.GetBytes((command + "\r\n").ToCharArray());
                clientSocket.Send(cmdBytes, cmdBytes.Length, 0);
                readReply();
            }

            private Socket createDataSocket()
            {
                sendCommand("PASV");

                if (retValue != 227)
                {
                    throw new IOException(reply.Substring(4));
                }

                int index1 = reply.IndexOf('(');
                int index2 = reply.IndexOf(')');
                string ipData = reply.Substring(index1 + 1, index2 - index1 - 1);
                int[] parts = new int[6];

                int len = ipData.Length;
                int partCount = 0;
                string buf = "";

                for (int i = 0; i < len && partCount <= 6; i++)
                {
                    char ch = Char.Parse(ipData.Substring(i, 1));
                    if (Char.IsDigit(ch))
                        buf += ch;
                    else if (ch != ',')
                    {
                        throw new IOException("Malformed PASV reply: " + reply);
                    }

                    if (ch == ',' || i + 1 == len)
                    {
                        try
                        {
                            parts[partCount++] = Int32.Parse(buf);
                            buf = "";
                        }
                        catch (Exception)
                        {
                            throw new IOException("Malformed PASV reply: " + reply);
                        }
                    }
                }

                string ipAddress = parts[0] + "." + parts[1] + "." + parts[2] + "." + parts[3];

                int port = (parts[4] << 8) + parts[5];

                Socket s = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                IPEndPoint ep = new IPEndPoint(Dns.Resolve(ipAddress).AddressList[0], port);

                try
                {
                    s.Connect(ep);
                }
                catch (Exception)
                {
                    throw new IOException("Can't connect to remote server");
                }
                return s;
            }
        }
    }

```

use of http://www.codeproject.com/Articles/31624/An-FTP-secure-client-library-for-C

origin - http://www.pipiscrew.com/?p=6231 c-ftpfactory