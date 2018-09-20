# Rosalind-learning 
Learning record 
# Rosalind 
# 1 DNA 
在R中Counting DNA Nucleotides 
#导入数据(txt文件格式),只有一行,直接用read.csv()函数导入即可. 
dna <- read.csv("rosalind_dna.txt",header = F) 
#此时的dna虽然只有一行,但是是data.frame,可以dna_vector <- as.vector(dan[1,]),转换成vector方便处理.这里一定要使用header = F,不然txt文件中唯一的一列会被当成标题,然后dna中就没有内容了. 
dna_vector <- as.vector(dan[1,]) 
#(1)  
dna_character <- strsplit(dna_vector,"") 
dna_count <- table(dna_character[[1]]) 
#或者把两个合并 
table(strsplit(d,”“)[[1]]) 
#(2) 使用stringr包
library(stringr) 
str_count(dna_vector,c(“A”,”C”,”G”,”T”)) 


