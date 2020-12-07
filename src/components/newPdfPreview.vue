<template>
    <div id="pdfContent" style="height:600px;width: 80%;margin: 0 auto">

    </div>
</template>
<script>
import PDFObject from "../../static/newPdf/pdfobject";
export default {
    name: '',
    mounted() {
        PDFObject.embed("https://pdfobject.com/pdf/sample-3pp.pdf", "#pdfContent");
    }
}
</script>
<style scoped>

</style>