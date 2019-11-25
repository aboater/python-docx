这个 Fork 主要添加了 commentsPart ，也就是说，**docx 可以使用批注啦！**

下面是一个简单的例子：

You can add comments to a document with this fork of the python-docx.

A simple demonstration is as follow:

```python
from docx import Document
from docx.shared import Inches
import time

document = Document()

heading = document.add_heading('Document Title', 0)
comment = document.add_comment_for(heading, "这是标题")
comment.author = "aboater"
comment.date = time.strftime("%Y-%m-%dT%H:%M:%S", time.localtime())

p = document.add_paragraph('A plain paragraph having some ')
p.add_run('bold').bold = True
run = p.add_run(' and some ')
p.add_run('italic.').italic = True

comment = document.add_comment_for(p, "这是段落")
comment.author = "aboater"
comment.date = time.strftime("%Y-%m-%dT%H:%M:%S", time.localtime())
print(comment.date)

comment = document.add_comment_for(run, "这是文字")
comment.author = "aboater"
comment.date = time.strftime("%Y-%m-%dT%H:%M:%S", time.localtime())

document.add_heading('Heading, level 1', level=1)
document.add_paragraph('Intense quote', style='Intense Quote')

document.add_paragraph(
    'first item in unordered list', style='List Bullet'
)
document.add_paragraph(
    'first item in ordered list', style='List Number'
)

records = (
    (3, '101', 'Spam'),
    (7, '422', 'Eggs'),
    (4, '631', 'Spam, spam, eggs, and spam')
)

table = document.add_table(rows=1, cols=3)

comment = document.add_comment_for(table, "这是表格")
comment.author = "aboater"
comment.date = time.strftime("%Y-%m-%dT%H:%M:%S", time.localtime())

print(document.remove_comment_of(table))

hdr_cells = table.rows[0].cells
hdr_cells[0].text = 'Qty'
hdr_cells[1].text = 'Id'
hdr_cells[2].text = 'Desc'

for qty, id, desc in records:
    row_cells = table.add_row().cells
    row_cells[0].text = str(qty)
    row_cells[1].text = id
    row_cells[2].text = desc
    comment = document.add_comment_for(row_cells[2], "这是表格的一个空格")
    comment.author = "aboater"
    comment.date = time.strftime("%Y-%m-%dT%H:%M:%S", time.localtime())
    print(comment.date)
    print(document.remove_comment_of(row_cells[2]))


document.add_page_break()

document.save('demo.docx')
```



更多教程请点击[原作者的教程](https://python-docx.readthedocs.io/en/latest/)。

More information is available in the [python-docx documentation](https://python-docx.readthedocs.org/en/latest/).



