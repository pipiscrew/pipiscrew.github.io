---
title: PHP | android | CSharp - Registration Validation / Safe Transcactions
author: PipisCrew
date: 2014-11-08
categories: []
toc: true
---

//CSharp
```js

            //this entered at registration dialog   
            //username=x@x.com
            //password=111-111-111
            //salt=your_name_here

        private void button1_Click(object sender, EventArgs e)
        {
            HTTPRequest request = new HTTPRequest("http://x.com/testAREA/lic.php", "POST", "e=x@x.com&s=111-111-111");

            if (request.GetResponse() == genLicenseVerification("x@x.com", "111-111-111"))
                MessageBox.Show("Success");
            else
                MessageBox.Show("Wrong");

        }

        private string genLicenseVerification(string email, string serial)
        {
            return this.GetMD5Hash("your_name_here" + email + serial);
        }

        public string GetMD5Hash(string input)
        {
            MD5CryptoServiceProvider provider = new MD5CryptoServiceProvider();
            byte[] bytes = Encoding.UTF8.GetBytes(input);
            bytes = provider.ComputeHash(bytes);
            StringBuilder builder = new StringBuilder();
            foreach (byte num in bytes)
            {
                builder.Append(num.ToString("x2").ToLower());
            }
            return builder.ToString();
        }

    public class HTTPRequest
    {

        private Stream dataStream;
        private WebRequest request;
        private string status;

        public HTTPRequest(string url)
        {
            this.request = WebRequest.Create(url);
        }

        public HTTPRequest(string url, string method) : this(url)
        {
            if (!method.Equals("GET") && !method.Equals("POST"))
            {
                throw new Exception("Invalid Method Type");
            }
            this.request.Method = method;
        }

        public HTTPRequest(string url, string method, string data) : this(url, method)
        {
            string s = data;
            byte[] bytes = Encoding.UTF8.GetBytes(s);
            this.request.ContentType = "application/x-www-form-urlencoded";
            this.request.ContentLength = bytes.Length;
            this.dataStream = this.request.GetRequestStream();
            this.dataStream.Write(bytes, 0, bytes.Length);
            this.dataStream.Close();
        }

        public string GetResponse()
        {
            WebResponse response = this.request.GetResponse();
            this.Status = ((HttpWebResponse)response).StatusDescription;
            this.dataStream = response.GetResponseStream();
            StreamReader reader = new StreamReader(this.dataStream);
            string str = reader.ReadToEnd();
            reader.Close();
            this.dataStream.Close();
            response.Close();
            return str;
        }

        public string Status
        {
            get
            {
                return this.status;
            }
            set
            {
                this.status = value;
            }
        }
    }
```

//android
```js
//at activity button
	public void btnAdd_Click(View view)
	{

			ArrayList<namevaluepair> nameValuePairs = new ArrayList<namevaluepair>();

			nameValuePairs.add(new BasicNameValuePair("e", "x@x.com"));
			nameValuePairs.add(new BasicNameValuePair("s", "111-111-111"));

			CustomHttpTask poster = new CustomHttpTask();
			poster.setHTTP_Method(CustomHttpTask.httpMethod.POST);
			poster.setNameValuePairs(nameValuePairs);

			poster.setListener(new IAsyncFetchListener() {

				@Override
				public void onComplete(String item) {
					final String tmp = item;

					runOnUiThread(new Runnable() { // manipulate GUI
						public void run() {
							try {
							if (md5("your_name_here" + "x@x.com" + "111-111-111").equalsIgnoreCase(tmp))
								Toast.makeText(getBaseContext(), "Success", Toast.LENGTH_LONG).show();
							else 
								Toast.makeText(getBaseContext(), "Wrong", Toast.LENGTH_LONG).show();
						} catch (NoSuchAlgorithmException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
						}
					});
				}

			});

			poster.execute("http://x.com/testAREA/lic.php");
	}

//the class
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.UnsupportedEncodingException;
import java.util.ArrayList;
import java.util.EventListener;

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.params.BasicHttpParams;

import android.os.AsyncTask;

public class CustomHttpTask extends AsyncTask<object, string,="" void=""> {

	// ////////////// HTTP METHOD ENUM
	public enum httpMethod {
		GET, POST
	}

	private httpMethod HTTP_Method;

	public httpMethod getHTTP_Method() {
		return HTTP_Method;
	}

	public void setHTTP_Method(httpMethod hTTP_Method) {
		HTTP_Method = hTTP_Method;
	}

	// ////////////// POST PAIRS
	private ArrayList<namevaluepair> nameValuePairs = null;

	public ArrayList<namevaluepair> getNameValuePairs() {
		return nameValuePairs;
	}

	public void setNameValuePairs(ArrayList<namevaluepair> nameValuePairs) {
		this.nameValuePairs = nameValuePairs;
	}

	// ////////////// EVENT
	// base event
	public interface IAsyncFetchListener extends EventListener {
		void onComplete(String item);
	}

	// base listener
	public void setListener(IAsyncFetchListener listener) {
		this.fetchListener = listener;
	}

	IAsyncFetchListener fetchListener = null;

	private String response = null;

	@Override
	protected Void doInBackground(Object... params) {
		String url = (String) params[0];

		try {
			if (HTTP_Method == httpMethod.GET)
				response = new URLReader().getResponse(url);
			else
				response = new URLPoster().getPost(url, nameValuePairs);

		} catch (Exception e) {
			response = null;
		}

		if (this.fetchListener != null)
			this.fetchListener.onComplete(response);

		return null;
	}

	private class URLPoster {

		public String getPost(String URL, ArrayList<namevaluepair> vars) {
			InputStream inputStream = null;
			HttpClient httpClient = new DefaultHttpClient();
			try {
				HttpPost post = (HttpPost) createNameValuePairEntity(nameValuePairs, URL);

				HttpResponse response = httpClient.execute(post);

				inputStream = response.getEntity().getContent(); // Get the data
																	// in the
																	// entity
				String ja = convertStreamToString(inputStream);

				return ja;

			} catch (Exception e) {
				return null;
			} finally {
				try {

					if (inputStream != null)
						inputStream.close();

				} catch (Exception squish) {
				}
			}
		}

		private String convertStreamToString(java.io.InputStream is) {
			java.util.Scanner s = new java.util.Scanner(is).useDelimiter("\\A");
			return s.hasNext() ? s.next() : "";
		}

		// for name pair
		private HttpUriRequest createNameValuePairEntity(ArrayList<namevaluepair> nameValuePairs, String url) {
			HttpPost post = null;
			try {
				post = new HttpPost(url);
				post.setEntity(new UrlEncodedFormEntity(nameValuePairs));
			} catch (Exception ex) {

			}
			return post;
		}

		// for JSON OBJ [start]
		// the call will be HttpPost post = (HttpPost)
		// createPostForJSONObject(json, "https://android.googleapis.com/gcm/send");
		private HttpUriRequest createPostForJSONObject(String params, String url) {
			HttpPost post = new HttpPost(url);
			post.setEntity(createStringEntity(params));
			return post;
		}

		private HttpEntity createStringEntity(String params) {
			StringEntity se = null;
			try {
				se = new StringEntity(params.toString(), "UTF-8");
				se.setContentType("application/json; charset=UTF-8");
			} catch (UnsupportedEncodingException e) {

			}
			return se;
		}
		// for JSON OBJ [end]
	}

	private class URLReader {

		public String getResponse(String URL) {
			InputStream inputStream = null;

			try {
				DefaultHttpClient httpclient = new DefaultHttpClient(new BasicHttpParams());
				HttpGet httpGetRequest = new HttpGet(URL);

				HttpResponse response = httpclient.execute(httpGetRequest);
				HttpEntity entity = response.getEntity();

				inputStream = entity.getContent();
				// json is UTF-8 by default
				BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"), 8);
				StringBuilder sb = new StringBuilder();

				String line = null;
				while ((line = reader.readLine()) != null)
					sb.append(line + "\n");

				return sb.toString();

			} catch (Exception e) {
				return null;
			} finally {
				try {

					if (inputStream != null)
						inputStream.close();

				} catch (Exception squish) {
				}
			}

		}
	}
}

```

//PHP

```js
<?php check="" for="" valid="" post="" if="" (!isset($_post["e"])="" ||="" !isset($_post["s"]))="" {="" echo="" "no="" valid="" post";="" exit;="" }="" calculate="" the="" md5="" $reg_code="md5(" your_name_here".$_post["e"].$_post["s"]);"="" return="" back="" echo="" $reg_code;=""?>
```

^to constructed as :
[![](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap221.png "snap221")](https://www.pipiscrew.com/wp-content/uploads/2014/11/snap221.png)</namevaluepair></namevaluepair></namevaluepair></namevaluepair></namevaluepair></object,></namevaluepair></namevaluepair>

origin - http://www.pipiscrew.com/?p=1752 php-android-csharp-registration-validation