# c++ for loops

_Status: Published_
_Created: 2016-04-11 04:56:46_
_Tags: c++_

<code>

char s[] = "string";
  printf("string is %s\n",s);
  for (int i = 0 ; s[i]; i++)
  {
    printf("string is %c\n",s[i]);
  }
  printf("---\n");
  for (char *cp=s;*cp;++cp)
  {
    printf("string is %c\n",*cp);
  }
  printf("---\n");
  for (char c: s)
  {
    if (c==0)break;// extra element 0!!so break!!
    printf("string is %c\n",c);
  }// extra element 0!!
</code>