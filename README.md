# KMP-Algorithm

玩了一天游戏，减轻一下负罪感

```
Python 3.10.9 (main, Dec 08 2022, 14:49:06) [GCC] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from kmp import *
>>> text="dhiufhaiudhsajiufdsaonjxiusddfiufsajnqwdn"
>>> KMP(text,"iuf").match()

index=2:
dh [ iuf ] haiudhsajiufdsaonjxiusddfiufsajnqwdn

next or stop?(n,s): n

index=14:
dhiufhaiudhsaj [ iuf ] dsaonjxiusddfiufsajnqwdn

next or stop?(n,s): n

index=30:
dhiufhaiudhsajiufdsaonjxiusddf [ iuf ] sajnqwdn

next or stop?(n,s): n
Not found!
>>> 

```
#### source

```python3

class pattern_matching:
    def __init__(self,text,pattern):
        self.text=text
        self.pattern=pattern

#Knuth-Morris-Pratt Algorithm
class KMP(pattern_matching):

    #The Partial Match Table
    def match_table(self):
        table=[0]
        for i in range(2,len(self.pattern)+1):
            s=self.pattern[:i]
            val=0
            for j in range(1,i):
                if s[:j]==s[-j:]:
                    val=max(val,len(s[:j]))
            table+=[val]
        return table

    def match(self):
        table=self.match_table()
        l_t,l_p=len(self.text),len(self.pattern)
        i=0

        while i<l_t:
            j=0
            matched=0
            leap=False

            while self.text[i]==self.pattern[j]:
                if j==l_p-1:
                    print("\nindex="+str(i-l_p+1)+':\n'+self.text[:i-l_p+1],'[',self.pattern,']',self.text[i+1:])
                    select=input("\nnext or stop?(n,s): ")
                    if select=='n':
                        break
                    else:
                        return
                i+=1
                j+=1
                matched+=1
                leap=True

            if leap:
                i+=matched-table[matched]
            else:
                i+=1

        print("Not found!")
        return
 ```
