npm i pdfjs-dist

```
const pdfjsLib = require('pdfjs-dist');
const fs = require("fs")

async function convertPdfToTxt(pdfPath, txtPath) {
  const data = new Uint8Array(fs.readFileSync(pdfPath));
  const loadingTask = pdfjsLib.getDocument(data);

  const pdf = await loadingTask.promise;
  const totalNumPages = pdf.numPages;

  let txtContent = '';

  for (let pageNum = 1; pageNum <= totalNumPages; pageNum++) {
    const page = await pdf.getPage(pageNum);
    const textContent = await page.getTextContent();
    const textItems = textContent.items;

    for (let i = 0; i < textItems.length; i++) {
      const item = textItems[i];
      txtContent += item.str + ' ';
    }

    txtContent += '\n';
  }

  fs.writeFileSync(txtPath, txtContent);
}

const pdfPath = 'C:xxxxx/ming.pdf';
const txtPath = 'C:xxxxx/pdfccc.txt';

convertPdfToTxt(pdfPath, txtPath)
.then(() => {
  console.log('PDF转换成功！');
})
.catch((error) => {
  console.error('PDF转换失败：', error);
});
```