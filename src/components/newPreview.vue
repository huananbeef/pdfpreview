<template>
    <div>
        <div class="contract-modal" id="contractDetail">
            <div id="mycanvas" ref="mycanvas"></div>
        </div>
    </div>
</template>
<script>
import pdf from '../../static/newPdf/pdf.js';
export default {
    name: 'pdfpreview',
    data(){
        return {
            visible: false
        }
    },
    mounted(){
            this.visible = true;
            this.getPdf()
    },
    methods: {
        getPdf(){
        // 此中方式接受流形式返回
            this.$refs.mycanvas.scrollTop =0
        //    let accessToken = cache.get('TOKEN').Authorization
        //    let url = `${config.baseUrls}/api/fund/v1/contractReports/previewContractContent?access_token=${accessToken}&id=${contractData.id}&contractUrl=${contractData.contractUrl}&.pdf`
            // let url = 'http://image.cache.timepack.cn/nodejs.pdf'
            let url = '/static/newPdf/111.pdf'
            let pdfjsLib = pdf
            console.log('---pdf---', pdf.PDFJS)
            pdfjsLib.PDFJS.workerSrc = '/static/newPdf/pdf.worker.js'
            // pdfjsLib.GlobalWorkerOptions.workerSrc = '/static/newPdf/pdf.worker.js'
            let loadingTask = pdfjsLib.getDocument(url)
            loadingTask.promise.then((pdf) =>{
                let numPages = pdf.numPages
                let container = document.getElementById('mycanvas')
                let pageNumber = 1
                this.getPage(pdf,pageNumber,container,numPages)
            }, function (reason) {
                alert(reason)
            });
        },
        getPage (pdf,pageNumber,container,numPages) { //获取pdf
            let pageRendering = true;
            let _this = this;
            pdf.getPage(pageNumber).then((page) => {
            let scale = (container.offsetWidth/page.view[2])
            let viewport = page.getViewport(scale)
            let canvas = document.createElement("canvas")
            canvas.width= viewport.width
            canvas.height= viewport.height
            container.appendChild(canvas)
            let ctx = canvas.getContext('2d');
            var renderContext = {
                canvasContext: ctx,
                transform: [1, 0, 0, 1, 0, 0],
                viewport: viewport,
                intent: 'print'
            };
            page.render(renderContext).then(() => {
                pageNumber +=1
                if(pageNumber<=numPages) {
                    _this.getPage(pdf,pageNumber,container,numPages)
                }
            })
        })
     }
    }
}
</script>
<style scoped>
    .contract-modal {
        position: absolute;
        right: 0;
        width: 100vw;
        height: 100vh;
        overflow: scroll;
        z-index: 900;
    }
    .contract-modal .contract-detail {
        margin: 0 auto;
        max-width: 96%;
        height: auto;
    }
    .contract-btns{
        height: 50px;
        background-color:  #fff;
        text-align: center;
        padding-bottom:44px;
        padding-top:10px;
    }
    #mycanvas {
        min-height: 50vh;
        background: #fff;
    }
    canvas{
        margin: 0 auto;
        display: block;
        border-bottom:2px solid #aaa;
    }
    .close-btn{
        position: absolute;
        right: 15%;
        width: 26px;
        height: 26px;
        z-index: 999;
        background-color: #666;
        border-radius: 50%;
        cursor: pointer;
    }
</style>
