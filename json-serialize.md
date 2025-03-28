# Json serialize

_Status: Published_
_Created: 2020-04-01 16:56:10_
_Tags: dotnet core, dotnet, .net_

<code>
using System;
using System.IO;
using System.Text.Json;
using System.Collections.Generic;
					
public class Program
{
	public class MyModel
{
    public string MyString { get; set; }
    public int MyInt { get; set; }
    public bool MyBoolean { get; set; }
    public decimal MyDecimal { get; set; }
    public DateTime MyDateTime1 { get; set; }
    public DateTime MyDateTime2 { get; set; }
    public List<string> MyStringList { get; set; }
    public Dictionary<string, Person> MyDictionary { get; set; }
    public MyModel MyAnotherModel { get; set; }
}

public class Person
{
    public int Id { get; set; }
    public string Name { get; set; }
}
	public static void Main()
	{
		var options = new JsonSerializerOptions
		{
    		PropertyNamingPolicy = JsonNamingPolicy.CamelCase,
    		WriteIndented = true
		};
		Person p = new Person();
		p.Id = 1;
		p.Name = "HJH";
		MyModel mm = new MyModel();
		mm.MyInt = 1;
		mm.MyBoolean = false;
		mm.MyString = "string";
		
		string s = JsonSerializer.Serialize(p, options);
		Console.WriteLine(s);
		string s2 = JsonSerializer.Serialize(mm, options);
		Console.WriteLine(s2);
	}
}
</code>