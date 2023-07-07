# read-pdf-without-any-download-button

<code>
  <script src="https://mozilla.github.io/pdf.js/build/pdf.js"></script>
<div id="pdfContainer"></div>

<script>
  // Path to the PDF file
  var pdfFile = 'test.pdf';

  // Load and render the PDF
  pdfjsLib.getDocument(pdfFile).promise.then(function(pdf) {
    var pdfContainer = document.getElementById('pdfContainer');

    // Iterate over each page
    for (var pageNumber = 1; pageNumber <= pdf.numPages; pageNumber++) {
      pdf.getPage(pageNumber).then(function(page) {
        var scale = 1.5;
        var viewport = page.getViewport({ scale: scale });

        // Prepare the canvas element
        var canvas = document.createElement('canvas');
        var context = canvas.getContext('2d');
        canvas.width = viewport.width;
        canvas.height = viewport.height;

        // Render the PDF page on the canvas
        var renderContext = {
          canvasContext: context,
          viewport: viewport
        };
        page.render(renderContext);

        // Append the canvas to the PDF container
        pdfContainer.appendChild(canvas);
      });
    }
  });
</script>

<style>
    #pdfContainer {
    max-width: 500px;
    background: red;
    overflow: scroll;
    background-size: cover; 
    background-attachment: fixed
}
#pdfContainer canvas {
    max-width: 100%;
}
</style>
</code>
