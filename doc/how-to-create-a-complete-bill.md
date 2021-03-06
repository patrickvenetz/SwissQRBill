# How to create a complete bill

### Introduction

In this manual you will learn how you can use SwissQRBill to create a complete PDF file and then attach the QR slip to the bottom of the page. We will use some methods from the PDFKit module as well as some methods from SwissQRBill which extends PDFKit functionality with different methods.

The methods used from PDFKit are documented on [pdfkit.org](http://pdfkit.org/docs/getting_started.html)<br/>
The methods used from SwissQRBill are documented in the [API documentation](https://github.com/schoero/SwissQRBill/blob/master/doc/api.md).


### Setup

If you haven't already done so, please install the library using:

```
npm i swissqrbill --save
```

Then you are able to include SwissQRBill to your project.

```js
const SwissQRBill = require("swissqrbill");
```

Once everything is set up we can start with creating a data object which contains the necessarry payment informations. These informations could be generated automatically by your program, or be retreived from your database.

```js
const data = {
  currency: "CHF",
  amount: 2606.35,
  reference: "210000000003139471430009017",
  creditor: {
    name: "SwissQRBill",
    address: "Bahnhofstrasse 7",
    zip: 1234,
    city: "Musterstadt",
    account: "CH4431999123000889012",
    country: "CH"
  },
  debtor: {
    name: "Pia-Maria Rutschmann-Schnyder",
    address: "Grosse Marktgasse 28",
    zip: 9400,
    city: "Rorschach",
    country: "CH"
  }
};
```


### Creating the PDF

Once we have our data ready we can create a new instance of `SwissQRBill` and store it to the variable `pdf`.

```js

const pdf = new SwissQRBill.PDF(data, "complete-qr-bill.pdf", { autoGenerate: false, size: "A4" });
```

Please note that we have set `autoGenerate` to `false` and `size` to `A4`.
This will create a PDF with the filename `complete-bill.pdf` without finalizing the document, so that we are able to add content to it.


### Adding our logo

We can add images as vector paths to the document using `addPath()`. You can find tools to convert your normal SVG files to vector paths online.

```js
const logoCross = "M16.8 2.8h1.4v1.4h-1.4zM19.6 2.8h1.4v1.4h-1.4zM16.8 4.2h1.4v1.4h-1.4zM18.2 4.2h1.4v1.4h-1.4zM19.6 4.2h1.4v1.4h-1.4zM19.6 5.6h1.4v1.4h-1.4zM18.2 7h1.4v1.4h-1.4zM19.6 7h1.4v1.4h-1.4zM14 8.4h1.4v1.4h-1.4zM15.4 8.4h1.4v1.4h-1.4zM16.8 8.4h1.4v1.4h-1.4zM14 9.8h1.4v1.4h-1.4zM15.4 9.8h1.4v1.4h-1.4zM16.8 9.8h1.4v1.4h-1.4zM19.6 9.8h1.4v1.4h-1.4zM14 11.2h1.4v1.4h-1.4zM16.8 11.2h1.4v1.4h-1.4zM19.6 11.2h1.4v1.4h-1.4zM18.2 12.6h1.4v1.4h-1.4zM19.6 12.6h1.4v1.4h-1.4zM4.2 14h1.4v1.4H4.2zM5.6 14h1.4v1.4H5.6zM7 14h1.4v1.4h-1.4zM8.4 14h1.4v1.4h-1.4zM9.8 14h1.4v1.4h-1.4zM11.2 14h1.4v1.4h-1.4zM12.6 14h1.4v1.4h-1.4zM15.4 14h1.4v1.4h-1.4zM16.8 14h1.4v1.4h-1.4zM23.8 14h1.4v1.4h-1.4zM25.2 14h1.4v1.4h-1.4zM30.8 14h1.4v1.4h-1.4zM2.8 15.4h1.4v1.4H2.8zM4.2 15.4h1.4v1.4H4.2zM7 15.4h1.4v1.4h-1.4zM12.6 15.4h1.4v1.4h-1.4zM14 15.4h1.4v1.4h-1.4zM15.4 15.4h1.4v1.4h-1.4zM18.2 15.4h1.4v1.4h-1.4zM19.6 15.4h1.4v1.4h-1.4zM23.8 15.4h1.4v1.4h-1.4zM26.6 15.4h1.4v1.4h-1.4zM28 15.4h1.4v1.4h-1.4zM29.4 15.4h1.4v1.4h-1.4zM30.8 15.4h1.4v1.4h-1.4zM4.2 16.8h1.4v1.4H4.2zM9.8 16.8h1.4v1.4h-1.4zM11.2 16.8h1.4v1.4h-1.4zM15.4 16.8h1.4v1.4h-1.4zM19.6 16.8h1.4v1.4h-1.4zM22.4 16.8h1.4v1.4h-1.4zM26.6 16.8h1.4v1.4h-1.4zM29.4 16.8h1.4v1.4h-1.4zM2.8 18.2h1.4v1.4H2.8zM7 18.2h1.4v1.4h-1.4zM16.8 18.2h1.4v1.4h-1.4zM19.6 18.2h1.4v1.4h-1.4zM21 18.2h1.4v1.4h-1.4zM23.8 18.2h1.4v1.4h-1.4zM25.2 18.2h1.4v1.4h-1.4zM26.6 18.2h1.4v1.4h-1.4zM28 18.2h1.4v1.4h-1.4zM29.4 18.2h1.4v1.4h-1.4zM30.8 18.2h1.4v1.4h-1.4zM4.2 19.6h1.4v1.4H4.2zM5.6 19.6h1.4v1.4H5.6zM7 19.6h1.4v1.4h-1.4zM8.4 19.6h1.4v1.4h-1.4zM9.8 19.6h1.4v1.4h-1.4zM11.2 19.6h1.4v1.4h-1.4zM14 19.6h1.4v1.4h-1.4zM15.4 19.6h1.4v1.4h-1.4zM19.6 19.6h1.4v1.4h-1.4zM14 21h1.4v1.4h-1.4zM16.8 21h1.4v1.4h-1.4zM18.2 21h1.4v1.4h-1.4zM14 22.4h1.4v1.4h-1.4zM15.4 22.4h1.4v1.4h-1.4zM16.8 22.4h1.4v1.4h-1.4zM14 23.8h1.4v1.4h-1.4zM18.2 23.8h1.4v1.4h-1.4zM14 25.2h1.4v1.4h-1.4zM16.8 25.2h1.4v1.4h-1.4zM19.6 25.2h1.4v1.4h-1.4zM14 26.6h1.4v1.4h-1.4zM15.4 26.6h1.4v1.4h-1.4zM16.8 26.6h1.4v1.4h-1.4zM19.6 26.6h1.4v1.4h-1.4zM14 28h1.4v1.4h-1.4zM15.4 28h1.4v1.4h-1.4zM16.8 28h1.4v1.4h-1.4zM19.6 28h1.4v1.4h-1.4zM14 29.4h1.4v1.4h-1.4zM15.4 29.4h1.4v1.4h-1.4zM16.8 29.4h1.4v1.4h-1.4zM19.6 29.4h1.4v1.4h-1.4z";
const logoBackground = "M0 0h35v35H0z";
const logoText = "M42.652 20.156c.058 1.029.301 1.865.729 2.507.815 1.203 2.253 1.804 4.311 1.804.923 0 1.763-.132 2.52-.395 1.466-.511 2.199-1.425 2.199-2.743 0-.988-.309-1.692-.926-2.112-.626-.412-1.606-.77-2.94-1.075l-2.459-.556c-1.605-.362-2.742-.761-3.409-1.198-1.153-.757-1.729-1.89-1.729-3.397 0-1.63.564-2.969 1.692-4.014 1.128-1.046 2.726-1.569 4.793-1.569 1.902 0 3.518.459 4.848 1.377 1.33.918 1.995 2.386 1.995 4.404h-2.31c-.123-.972-.387-1.717-.79-2.236-.75-.947-2.022-1.421-3.817-1.421-1.45 0-2.491.305-3.125.915-.635.609-.952 1.317-.952 2.124 0 .89.371 1.54 1.112 1.952.486.264 1.585.593 3.298.988l2.545.581c1.227.28 2.174.663 2.841 1.149 1.153.848 1.729 2.079 1.729 3.693 0 2.009-.73 3.446-2.192 4.311-1.462.865-3.16 1.297-5.096 1.297-2.256 0-4.023-.576-5.299-1.729-1.276-1.145-1.902-2.697-1.878-4.657h2.31zM58.649 12.781l2.545 10.426 2.582-10.426h2.495l2.594 10.364 2.705-10.364h2.224l-3.842 13.23h-2.31l-2.693-10.24-2.606 10.24h-2.31l-3.817-13.23h2.433zM75.894 12.843h2.26v13.168h-2.26V12.843zm0-4.978h2.26v2.52h-2.26v-2.52zM82.836 21.861c.066.741.251 1.309.556 1.704.56.717 1.531 1.075 2.915 1.075.823 0 1.548-.179 2.174-.537.626-.359.939-.913.939-1.662 0-.568-.251-1-.754-1.297-.321-.181-.955-.391-1.902-.63l-1.766-.445c-1.129-.28-1.96-.593-2.496-.938-.955-.602-1.433-1.433-1.433-2.496 0-1.251.451-2.264 1.353-3.038.902-.775 2.114-1.162 3.638-1.162 1.993 0 3.43.585 4.311 1.754.552.742.819 1.54.803 2.397h-2.1a2.572 2.572 0 0 0-.531-1.371c-.511-.585-1.396-.877-2.656-.877-.84 0-1.476.16-1.909.481-.432.322-.648.746-.648 1.273 0 .576.284 1.037.852 1.383.33.206.816.387 1.458.544l1.47.358c1.597.387 2.668.762 3.212 1.124.864.568 1.297 1.462 1.297 2.681 0 1.177-.447 2.194-1.341 3.051-.893.856-2.254 1.284-4.082 1.284-1.968 0-3.362-.446-4.182-1.34-.819-.893-1.258-1.999-1.315-3.316h2.137zM95.485 21.861c.066.741.251 1.309.556 1.704.56.717 1.532 1.075 2.915 1.075.824 0 1.548-.179 2.174-.537.626-.359.939-.913.939-1.662 0-.568-.251-1-.754-1.297-.321-.181-.955-.391-1.902-.63l-1.766-.445c-1.129-.28-1.96-.593-2.496-.938-.955-.602-1.432-1.433-1.432-2.496 0-1.251.45-2.264 1.352-3.038.902-.775 2.115-1.162 3.638-1.162 1.993 0 3.43.585 4.311 1.754.552.742.82 1.54.803 2.397h-2.1a2.572 2.572 0 0 0-.531-1.371c-.511-.585-1.396-.877-2.656-.877-.84 0-1.476.16-1.908.481-.433.322-.649.746-.649 1.273 0 .576.284 1.037.852 1.383.33.206.816.387 1.458.544l1.47.358c1.598.387 2.668.762 3.212 1.124.864.568 1.297 1.462 1.297 2.681 0 1.177-.447 2.194-1.341 3.051-.893.856-2.254 1.284-4.082 1.284-1.968 0-3.362-.446-4.181-1.34-.82-.893-1.258-1.999-1.316-3.316h2.137zM123.711 25.962l-1.235 1.494-2.804-2.137c-.676.371-1.407.667-2.193.89a9.454 9.454 0 0 1-2.576.333c-2.816 0-5.023-.922-6.621-2.767-1.408-1.795-2.112-4.043-2.112-6.744 0-2.454.609-4.554 1.828-6.3 1.565-2.24 3.879-3.36 6.943-3.36 3.203 0 5.575 1.029 7.115 3.088 1.202 1.606 1.803 3.66 1.803 6.164a13.02 13.02 0 0 1-.432 3.372c-.437 1.647-1.174 2.99-2.211 4.027l2.495 1.94zm-8.511-1.619c.51 0 .988-.035 1.433-.105.445-.07.832-.208 1.161-.413l-1.989-1.557 1.235-1.519 2.372 1.84a6.869 6.869 0 0 0 1.526-2.878c.267-1.062.401-2.079.401-3.051 0-2.133-.558-3.85-1.674-5.151-1.115-1.301-2.641-1.952-4.576-1.952-1.96 0-3.513.624-4.657 1.872-1.145 1.247-1.717 3.168-1.717 5.762 0 2.182.549 3.92 1.649 5.213 1.099 1.293 2.711 1.939 4.836 1.939zM135.224 16.178c1.153 0 2.065-.23 2.736-.691.671-.462 1.007-1.293 1.007-2.496 0-1.293-.47-2.174-1.409-2.643-.502-.247-1.173-.371-2.013-.371h-6.004v6.201h5.683zm-8.141-8.313h8.4c1.384 0 2.524.202 3.422.605 1.704.774 2.557 2.203 2.557 4.287 0 1.087-.225 1.976-.673 2.668-.449.691-1.077 1.247-1.884 1.667.708.289 1.241.667 1.599 1.137.359.469.558 1.231.6 2.285l.086 2.434c.025.691.082 1.206.173 1.544.148.576.412.947.791 1.111v.408h-3.015a2.259 2.259 0 0 1-.197-.605c-.05-.247-.091-.725-.124-1.433l-.148-3.027c-.058-1.185-.498-1.98-1.322-2.384-.469-.222-1.206-.333-2.211-.333h-5.596v7.782h-2.458V7.865zM151.875 15.536c1.038 0 1.845-.144 2.421-.432.906-.453 1.359-1.269 1.359-2.446 0-1.186-.482-1.985-1.445-2.397-.544-.23-1.351-.346-2.421-.346h-4.386v5.621h4.472zm.828 8.375c1.507 0 2.581-.436 3.224-1.309.403-.552.605-1.219.605-2.001 0-1.318-.589-2.216-1.766-2.693-.626-.256-1.454-.383-2.483-.383h-4.88v6.386h5.3zm-7.708-16.046h7.794c2.125 0 3.636.634 4.534 1.902.527.75.79 1.614.79 2.594 0 1.145-.325 2.084-.976 2.817-.337.387-.823.741-1.457 1.062.93.354 1.626.754 2.087 1.198.816.791 1.223 1.882 1.223 3.274 0 1.169-.366 2.227-1.099 3.174-1.095 1.417-2.837 2.125-5.225 2.125h-7.671V7.865zM161.634 12.843h2.26v13.168h-2.26V12.843zm0-4.978h2.26v2.52h-2.26v-2.52zM167.316 7.865h2.223v18.146h-2.223zM172.937 7.865h2.223v18.146h-2.223z";


pdf.addPath(logoBackground, SwissQRBill.utils.mmToPoints(20), SwissQRBill.utils.mmToPoints(14))
  .fillColor("#ad2328")
  .fill();

pdf.addPath(logoCross, SwissQRBill.utils.mmToPoints(20), SwissQRBill.utils.mmToPoints(14))
  .fillColor("white")
  .fill();

pdf.addPath(logoText, SwissQRBill.utils.mmToPoints(20), SwissQRBill.utils.mmToPoints(14))
  .fillColor("black")
  .fill();

```

We use the `SwissQRBill.mmToPoints()` method to place the logo 2cm from the left side and 14mm from the top. Then we fill the path with our colors.

### Adding the addresses

Next, we add the address of our business and the customer address to the PDF. You can use `\n` to create a new line.

```js
pdf.fontSize(12);
pdf.font("Helvetica");
pdf.text(data.creditor.name + "\n" + data.creditor.address + "\n" + data.creditor.zip + " " + data.creditor.city, SwissQRBill.utils.mmToPoints(20), SwissQRBill.utils.mmToPoints(35), {
  width: SwissQRBill.utils.mmToPoints(100),
  height: SwissQRBill.utils.mmToPoints(50),
  align: "left"
});

pdf.fontSize(12);
pdf.font("Helvetica");
pdf.text(data.debtor.name + "\n" + data.debtor.address + "\n" + data.debtor.zip + " " + data.debtor.city, SwissQRBill.utils.mmToPoints(130), SwissQRBill.utils.mmToPoints(60), {
  width: SwissQRBill.utils.mmToPoints(70),
  height: SwissQRBill.utils.mmToPoints(50),
  align: "left"
});

```


### Create a title and a date

```js
pdf.fontSize(14);
pdf.font("Helvetica-Bold");
pdf.text("Rechnung Nr. 1071672", SwissQRBill.utils.mmToPoints(20), SwissQRBill.utils.mmToPoints(100), {
  width: SwissQRBill.utils.mmToPoints(170),
  align: "left"
});

const date = new Date();

pdf.fontSize(11);
pdf.font("Helvetica");
pdf.text("Musterstadt " + date.getDate() + "." + (date.getMonth() + 1) + "." + date.getFullYear(), {
  width: SwissQRBill.utils.mmToPoints(170),
  align: "right"
});
```


### Adding a table

To create a table we can use the `addTable()` method.

```js
const table = {
  width: SwissQRBill.utils.mmToPoints(170),
  rows: [
    {
      height: 30,
      fillColor: "#ECF0F1",
      columns: [
        {
          text: "Position",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Anzahl",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Bezeichnung"
        }, {
          text: "Total",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      columns: [
        {
          text: "1",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "14 Std.",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Programmierung SwissQRBill"
        }, {
          text: "CHF 1'540.00",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      columns: [
        {
          text: "2",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "8 Std.",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Dokumentation"
        }, {
          text: "CHF 880.00",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      height: 40,
      columns: [
        {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Summe",
          font: "Helvetica-Bold"
        }, {
          text: "CHF 2'420.00",
          font: "Helvetica-Bold",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      columns: [
        {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "MwSt."
        }, {
          text: "7.7%",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      columns: [
        {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "MwSt. Betrag"
        }, {
          text: "CHF 186.35",
          width: SwissQRBill.utils.mmToPoints(30)
        }
      ]
    }, {
      height: 40,
      columns: [
        {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "",
          width: SwissQRBill.utils.mmToPoints(20)
        }, {
          text: "Rechnungstotal",
          font: "Helvetica-Bold"
        }, {
          text: "CHF 2'606.35",
          width: SwissQRBill.utils.mmToPoints(30),
          font: "Helvetica-Bold"
        }
      ]
    }
  ]
};

pdf.addTable(table);
```

### Adding the QR bill

When we call the `addQRBill()` method, SwissQRBill will automatically add the QR slip to the bottom of the current page if there is enough space left, otherwise it will generate a new page in the size of `A6/5`.

```js
pdf.addQRBill();
```

### Finalizing the document

Once our document is finished, we have to call the `end()` method to finalize the document. Otherwise it will not be possible to open the generated pdf file.

```js
pdf.end();
```

We also have to wait until the file has been finished writing before we are able to interact with the generated pdf file. We can do this either by passing a callback function as the last parameter to `new SwissQRBill()` or by listening for the `finish` event on the SwissQRBill instance. You can find examples using callbacks and events in [examples/callback.js](https://github.com/schoero/SwissQRBill/tree/master/examples/callback.js) and [examples/event.js](https://github.com/schoero/SwissQRBill/tree/master/examples/event.js)

The complete code can be found in [examples/how-to-create-a-complete-bill.js](https://github.com/schoero/SwissQRBill/tree/master/examples/how-to-create-a-complete-bill.js).

When you run the code above, SwissQRBill should generate a PDF file name complete-qr-bill.pdf that looks like this:

[<img src="https://raw.githubusercontent.com/schoero/SwissQRBill/master/assets/complete-qr-bill.png">](https://github.com/schoero/SwissQRBill/blob/master/assets/complete-qr-bill.pdf)