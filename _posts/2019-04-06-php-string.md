---
title: PHP string compress at gzip/bzip C# decompress
author: PipisCrew
date: 2019-04-06
categories: [php,.net]
toc: true
---

```js
if (JData["compression"].ToString() == "bzip")
	output = General.DecompressStringBZIP(JData["data"].ToString());
else if (JData["compression"].ToString() == "gzip")
	output = General.DecompressStringGZIP(JData["data"].ToString());
else if (JData["compression"].ToString() == "none")
	output = General.Base64Decode( JData["data"].ToString());

public static string DecompressStringBZIP(string compressedText)
	  {
		  //src - http://community.sharpdevelop.net/forums/t/11005.aspx
		  //tested with https://github.com/icsharpcode/SharpZipLib/releases/tag/0.86.0.518
		  Byte[] bytes = Convert.FromBase64String(compressedText);
		  MemoryStream memStream = new MemoryStream(bytes);
		  BZip2InputStream gzipStream = new BZip2InputStream(memStream);
		  byte[] data = new byte[2048];
		  char[] chars = new char[2048]; // must be at least as big as 'data'
		  Decoder decoder = Encoding.UTF8.GetDecoder();
		  StringBuilder sb = new StringBuilder();

		  while (true)
		  {
			  int size = gzipStream.Read(data, 0, data.Length);
			  if (size == 0)
				  break;
			  int n = decoder.GetChars(data, 0, size, chars, 0);
			  sb.Append(chars, 0, n);
		  }
		  return sb.ToString();

}

public static string DecompressStringGZIP(string compressedText)
{
	// src - https://stackoverflow.com/a/4080983
	byte[] gZipBuffer = Convert.FromBase64String(compressedText); 

	using (var mem = new MemoryStream())
	{
		mem.Write(new byte[] { 0x1f, 0x8b, 0x08, 0x00, 0x00, 0x00, 0x00, 0x00 }, 0, 8);
		mem.Write(gZipBuffer, 0, gZipBuffer.Length);

		mem.Position = 0;

		using (var gzip = new GZipStream(mem, CompressionMode.Decompress))
		using (var reader = new StreamReader(gzip))
		{
			return reader.ReadToEnd();
		}
	}
}

public static string Base64Decode(string base64EncodedData)
{
	var base64EncodedBytes = System.Convert.FromBase64String(base64EncodedData);
	return System.Text.Encoding.UTF8.GetString(base64EncodedBytes);
}
```

### PHP

```js
function send_to_client($val)
{
	$compression = "none";

	if (function_exists('bzcompress')) {
		$compression = "bzip";
		$val = bzcompress($val);
	} else if (function_exists('gzcompress')) {
		$compression = "gzip";
		$val = gzcompress($val);
	}

	echo json_encode(array("data" => base64_encode($val), "compression" => $compression));
}
```

origin - https://www.pipiscrew.com/?p=14810 php-string-compress-at-gzipbzip-c-decompress