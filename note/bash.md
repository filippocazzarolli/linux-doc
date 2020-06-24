## history
!! -> last command

!ls -> last ls comand

$_ -> last argument (mkdir test && cd $_)

$? -> exit code

$$ -> PID

## General
echo {1,2,3}

1 2 3

echo {100..110}

100 101 102 103 104 105 106 107 108 109 110

for i in * ; do echo "$i" ; done # list file in a dir

for i in ** ; do echo "$i" ; done # sub dir

## Variable
a=test <- string
a=`ls /home` <- result of command
echo ${x:-default} <- if x not exist return default value
echo ${x:=default} <- if x not exist return default value and assign value in var
echo ${x:+value} <- if exist assegn value
echo ${x:2:1} -> x=0123456789 return 2 (substring)
echo ${#x} <- retun length of x variable

[bob in ~] echo $STRING
thisisaverylongname
[bob in ~] echo ${STRING#this}
isaverylongname

[bob in ~] echo $STRING
thisisaverylongname
[bob in ~] echo ${STRING%name}
thisisaverylong

## Array
`fruit=(apple pear banana)`

`echo ${fruit[0]}` -> print first value

`echo ${fruit[*]}` -> print all array

`echo ${ARRAY[*]}` one two one three one four

`echo ${ARRAY[*]#one}` two three four

`echo ${ARRAY[*]#t}` one wo one hree one four

`echo ${ARRAY[*]#t*}` one wo one hree one four

`echo ${ARRAY[*]##t*}` one one one four

## Replace 
`my_var="Give me a banana banana"`

`echo ${my_var/banana/pera}` -> Give me a pera banana

`echo ${my_var//banana/pera}` -> Give me a pera pera

