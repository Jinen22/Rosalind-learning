# Rosalind-learning 
Learning record 
## Rosalind 
### 1 DNA -Counting DNA Nucleotides  
使用R语言完成一下题目  
```
#导入数据(txt文件格式),只有一行,直接用read.csv()函数导入即可.  
dna <- read.csv("rosalind_dna.txt",header = F)  
```
此时的dna虽然只有一行,但是是data.frame,可以dna_vector <- as.vector(dan[1,]),转换成vector方便处理.这里一定要使用header = F,不然txt文件中唯一的一列会被当成标题,然后dna中就没有内容了.  
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
3.Linux shell(学了很久的sed和awk终于可以用上了)
```
awk '{gsub(/T/,"U");print}' rosalind_rna.txt
#或者
sed does sed 's/T/U/g' rosalind_rna.txt
#以上方法都是引用自rosalind网站上他人已经提供的解决方法,作为初学者者,感觉大有裨益,因此记录一下,方便日后查看
```
