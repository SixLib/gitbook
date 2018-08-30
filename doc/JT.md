``` flow
st=>start: 开始
op=>operation: 投保
op1=>operation: 出单
cond=>condition: 是否投保成功?
cond1=>condition: 是否出单成功?
e=>end: 结束
st->op->cond
cond(yes)->op1->cond1
cond(no)->op
cond1(yes)->e
cond1(no)->op1
```