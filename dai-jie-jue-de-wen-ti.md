onClick={e=&gt;{e.preventDefault}}和\#

console.log\({...store.getState\(\)}\)能打印出东西，而console.log\(...store.getState\(\)\)打印不出东西

&lt;a {{...store.getState}}也打印不出东西&gt;

上面这两个问题应该和React的props设计有关

