#### Replace
1. Replace all occurances of a word
   sed 's/<find>/<replace>/' toppings.txt
2. Replace on a specific line number [2]
   sed '2 s/<find>/<replace>/' toppings.txt   
2. / -> delimeter, we can use anything / . | as delimeter
3. change delimeter, if find or replace word consists that delimeter
4. suppose we want to update /etc with blank 
   sed 's./etc..' dump1.txt
5. we can use pipe also 
   echo "hello" | sed 's/hello/goodbye/'

#### Filter
6. filter lines that consist a specific word
   sed -n '/<word>/p' toppings.txt
7. filter lines that does not consist a specific word
   sed '/<word>/d' toppings.txt
8. filter lines that start with a specific word
   sed -n '/^<word>/p' toppings.txt
9. filter lines that end with a specific word
   sed -n '/<word>$/p' toppings.txt

#### Get content by line number
7. content of a specific line [3 <- line no]
   sed -n '3p' toppings.txt 
8. get last line
   sed -n '$p' toppings.txt
9. get range of lines content [1 to 3 rd line]
   sed -n '1,3p' toppings.txt
10. 

### Multiple expression
10. filter line with any of the two words
    sed -n -e '/<word1>/p' -e '/<word2>/p' toppings.txt
