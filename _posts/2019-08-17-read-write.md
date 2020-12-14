---
title: Read write List of T to XML
author: PipisCrew
date: 2019-08-17
categories: [.net]
toc: true
---

The XMLHelper class.

```js
// src - https://stackoverflow.com/a/25369059/1320686

public static class XmlHelper
{
    public static bool NewLineOnAttributes { get; set; }
    /// <summary>
    /// Serializes an object to an XML string, using the specified namespaces.
    /// </summary>
    public static string ToXml(object obj, XmlSerializerNamespaces ns)
    {
        Type T = obj.GetType();

        var xs = new XmlSerializer(T);
        var ws = new XmlWriterSettings { Indent = true, NewLineOnAttributes = NewLineOnAttributes, OmitXmlDeclaration = true };

        var sb = new StringBuilder();
        using (XmlWriter writer = XmlWriter.Create(sb, ws))
        {
            xs.Serialize(writer, obj, ns);
        }
        return sb.ToString();
    }

    /// <summary>
    /// Serializes an object to an XML string.
    /// </summary>
    public static string ToXml(object obj)
    {
        var ns = new XmlSerializerNamespaces();
        ns.Add("", "");
        return ToXml(obj, ns);
    }

    /// <summary>
    /// Deserializes an object from an XML string.
    /// </summary>
    public static T FromXml<t>(string xml)
    {
        XmlSerializer xs = new XmlSerializer(typeof(T));
        using (StringReader sr = new StringReader(xml))
        {
            return (T)xs.Deserialize(sr);
        }
    }

    /// <summary>
    /// Deserializes an object from an XML string, using the specified type name.
    /// </summary>
    public static object FromXml(string xml, string typeName)
    {
        Type T = Type.GetType(typeName);
        XmlSerializer xs = new XmlSerializer(T);
        using (StringReader sr = new StringReader(xml))
        {
            return xs.Deserialize(sr);
        }
    }

    /// <summary>
    /// Serializes an object to an XML file.
    /// </summary>
    public static void ToXmlFile(Object obj, string filePath)
    {
        var xs = new XmlSerializer(obj.GetType());
        var ns = new XmlSerializerNamespaces();
        var ws = new XmlWriterSettings { Indent = true, NewLineOnAttributes = NewLineOnAttributes, OmitXmlDeclaration = true };
        ns.Add("", "");

        using (XmlWriter writer = XmlWriter.Create(filePath, ws))
        {
            xs.Serialize(writer, obj);
        }
    }

    /// <summary>
    /// Deserializes an object from an XML file.
    /// </summary>
    public static T FromXmlFile<t>(string filePath)
    {
        StreamReader sr = new StreamReader(filePath);
        try
        {
            var result = FromXml<t>(sr.ReadToEnd());
            return result;
        }
        catch (Exception e)
        {
            throw new Exception("There was an error attempting to read the file " + filePath + "\n\n" + e.InnerException.Message);
        }
        finally
        {
            sr.Close();
        }
    }
}
```

```js
public class Supplier
{
	public string CompanyName { get; set; }
	public string ContactName { get; set; }

	public string ContactTitle { get; set; }
	public string Address { get; set; }
}
```

save a list<t> to xml file
```js
List<supplier> c = new List<supplier> {
	new Supplier { Address = "1223 Clousson Road", CompanyName = "Iowa", ContactName = "Danbury",ContactTitle = "Ms"}, 
	new Supplier { Address = "3165 Star Route", CompanyName = "Bridgeview", ContactName = "Illinois",ContactTitle = "Mr"}
};

XmlHelper.ToXmlFile(c, @"x:\table.xml");
```

read XML file to list<t>
```js
var all = XmlHelper.FromXmlFile<><supplier>>(@"x:\table.xml");

Console.WriteLine(all);

var q = all.Where(x => x.CompanyName == "Iowa").FirstOrDefault();

Console.WriteLine(q);
```

![alt boooo](https://i.imgur.com/59HDJtV.png)

refs :
[https://www.dotnetcurry.com/linq/564/linq-to-xml-tutorials-examples](https://www.dotnetcurry.com/linq/564/linq-to-xml-tutorials-examples)
[https://blogs.msdn.microsoft.com/wriju/2008/03/24/linq-to-xml-join-xml-data/](https://blogs.msdn.microsoft.com/wriju/2008/03/24/linq-to-xml-join-xml-data/)
[https://orderofcode.com/2016/05/31/reading-big-xmls-in-net/](https://orderofcode.com/2016/05/31/reading-big-xmls-in-net/)</supplier></t></supplier></supplier></t></t></t></t>

origin - https://www.pipiscrew.com/?p=15221 read-write-list-of-t-to-xml