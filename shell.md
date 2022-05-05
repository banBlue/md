
#### 同一行运行多个命令
|命令| 描述
|:-|:-|
|A ; B|	执行A后不论A的返回结果接着执行B
|A && B |	执行A后，仅在A成功运行后执行B
|A \|\| B	|执行A后仅在A失败后执行A\
`例如:git add .&git commit -m .&git push`
