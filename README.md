<div align="center">

## C\# Chr and Asc Functions


</div>

### Description

C# lacks VB's Chr and Asc functions. Unfortunately, none of the C# implementations I've found actually create the undocumented VB functions. Here are the true implentation of those functions. Note that simply casting a value as a char does not work for the entire range of characters. To see what I mean, create a test program in VB and one in C#. Do a simple loop from 1 to 255 and print out the characters using VB's Chr functions and simple casting in C#. Even using the ASCII encoding won't work as one submission here clains. If you don't want to bother looping and comparing 255 characters, try just using 137 for a value. You'll soon see what I mean. VB's Chr function will return one value but casting or using the ASCII encoding in C# will return a different value. Not cool if you're writing you own encryption algorithm or other code where a VB object must communicate with a C# object. So here's the real, undocumented deal, that will save you many hours of frustration!
 
### More Info
 
A single string character (for the Asc function) or an integer (for the Chr function)

Add clsVB to your project. The methods are static so you can call them like this: myChar = clsVB.Chr(137) or myInt = clsVB.Asc("B")

An integer (for the Asc function) or a single character (for the Chr function)


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Darrell Sparti, MCSD](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/darrell-sparti-mcsd.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C\#
**Category**       |[Strings](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/strings__10-26.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/darrell-sparti-mcsd-c-chr-and-asc-functions__10-3828/archive/master.zip)





### Source Code

```
internal class clsVB
{
  internal static string Chr(int p_intByte)
  {
   if( (p_intByte < 0) || (p_intByte > 255) )
   {
     throw new ArgumentOutOfRangeException("p_intByte", p_intByte, "Must be between 1 and 255.");
   }
   byte[] bytBuffer = new byte[]{(byte) p_intByte};
   return Encoding.GetEncoding(1252).GetString(bytBuffer);
  }
  internal static int Asc(string p_strChar)
  {
   if( (p_strChar.Length == 0) || (p_strChar.Length > 1) )
   {
     throw new ArgumentOutOfRangeException("p_strChar", p_strChar, "Must be a single character.");
   }
   char[] chrBuffer = {Convert.ToChar(p_strChar)};
   byte[] bytBuffer = Encoding.GetEncoding(1252).GetBytes(chrBuffer);
   return (int) bytBuffer[0];
  }
}
```

