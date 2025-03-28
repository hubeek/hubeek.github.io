# add folder

_Status: Published_
_Created: 2014-09-04 06:17:11_
_Tags: .net_

<code>if (!Directory.Exists(path)) 
{
  DirectoryInfo di = Directory.CreateDirectory(path);
}
</code>