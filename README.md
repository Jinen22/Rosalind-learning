# Rosalind-learning 
Learning record 
## Rosalind 
### 1 DNA -Counting DNA Nucleotides  
使用R语言完成一下题目  
```
#导入数据(txt文件格式),只有一行,直接用read.csv()函数导入即可.  
dna <- read.csv("rosalind_dna.txt",header = F)  
```
此时的dna虽然只有一行,但是仍然是data.frame,可以dna_vector <- as.vector(dan[1,]),转换成vector方便处理.这里一定要使用header = F,不然txt文件中唯一的一列会被当成标题,然后dna中就没有内容了.  
```
dna_vector <- as.vector(dan[1,])  
#(1)使用strsplit和table   
dna_character <- strsplit(dna_vector,"")  
dna_count <- table(dna_character[[1]])  
#或者把两个合并  
table(strsplit(d,”“)[[1]])  
#(2) 使用stringr包 
library(stringr)  
str_count(dna_vector,c(“A”,”C”,”G”,”T”))  
```
### 2 RNA -Transcribing DNA into RNA
1.python3  
```
str = 'GATGGAACTTGACT'
print (str.replace('T','U'))
```  
2.R
```
seq <- "GATGGAACTTGACTACGTAAATT"
gsub("T","U",seq)
```
3.Bash(学了很久的sed和gawk终于可以用上了)
```
awk '{gsub(/T/,"U");print}' rosalind_rna.txt
#或者
sed does sed 's/T/U/g' rosalind_rna.txt
#以上方法都是引用自rosalind网站上他人已经提供的解决方法,作为初学者,感觉大有裨益,因此记录一下,方便日后查看
```
### 3 Complementing a Strand of DNA
1.python3
```
#导入DNA序列
filename = 'rosalind_revc.txt'
with open(filename) as file_object:
    lines = file_object.readlines()

seq = ''
for line in lines:
    seq += line.strip()
#检查一下序列是否正确导入
print(seq)
print(len(seq))

# Complementing a Strand of DNA
rev_seq=seq[::-1].replace('C', 'g').replace('G', 'c').replace('T', 'a').replace('A', 't').upper()
print(rev_seq)
```
或者在数据导入之后,考虑到这种转换会很常用,可以建立一个函数,方便以后调用
```
def reverse(seq):
    dict = {'A': 'T', 'C': 'G', 'T': 'A', 'G': 'C'}
 
    revSeqList = list(reversed(seq))                #['T', 'G', 'G', 'C', 'C', 'C', 'A', 'A', 'A', 'A']
    revComSeqList = [dict[k] for k in revSeqList]  # ['A', 'C', 'C', 'G', 'G', 'G', 'T', 'T', 'T', 'T']
    revComSeq = ''.join(revComSeqList)             # ACCGGGTTTT
    return revComSeq

print(reverse(seq))
#链接：https://www.jianshu.com/p/339973874490
```
2.bash(以前一直没有发现sed和awk竟然有如此丰富的应用)
```
rev /path/to/file | sed 'y/ATCG/TAGC/'
#或者直接使用tr函数
rev r.txt | tr ATCG TAGC
# for multi lines
tr -d "\n" < r.txt| rev  | tr ATCG TAGC
```
使用bash写出来的语句看着非常简短优雅,所以linux shell中的常用函数还是要熟练掌握啊.

### 4 Counting Point Mutations
1.R
```
string <- read.csv("rosalind_hamm.txt",header = F)

string_vector_a <- strsplit(as.vector(string[1,]),"")
string_vector_b <- strsplit(as.vector(string[2,]),"")

string_vector_a <- as.vector(string_vector_a[[1]])
string_vector_b <- as.vector(string_vector_b[[1]])

sum = 0
i = 1
while (i <= length(string_vector_a)){
  if (string_vector_a[i] != string_vector_b[i]){
    sum = sum +1
  }
  i = i + 1
}
sum
```
2.python
```
cnt = 0
for i in range(len(a)):
    if a[i] != b[i]: cnt+=1
print cnt
#这里使用python可以直接访问字符串,比R中更方便一些
```
### 5 Rabbits and Recurrence Relations
1. Solution in R
```
#题目说明里已经介绍的非常清楚了，考察函数的递归。具体使用时把k换成具体给定的数据就可以了。
fibo <- function(n) {
  if(n == 1 | n == 2) {
    return(1)
  }
  else {
    return(fibo(n-1) + k * fibo(n-2))
  }
}
```
然后根据给定的n和k值，进行计算。
```
fibo(n)
```
