<template>
    <div id="app">
        <div class="container-fluid">
            <div class="h2 text-center mt-5">List with DnD practice</div>
            <section v-for="index in howManyCate" :key="index">
                <DndView :msg="`Sequence ${index}`"/>
                <hr>
            </section>
            <div class="mt-3 mb-3">
                <button class="btn btn-dark btn-lg" @click.stop.prevent="add">
                    create category ({{ maxCate - howManyCate }} remaining)
                </button>
            </div>
            <div class="mt-3 mb-3 text-right">
                <div class="btn btn-primary" @click.prevent.stop="capture">Finish</div>
            </div>
            </div>
            <div class="bg-light">
                <div class="container text-center p-2">
                This is footer.
            </div>
        </div>
    </div>
</template>

<script>
import html2canvas from 'html2canvas';
import DndView from './components/DndView.vue'

export default {
    name: 'app',
    components: {
        DndView
    },
    data() {
        return {
            maxCate: 5,
            howManyCate: 1
        }
    },
    mounted() {
        window.onbeforeunload = function() {
            if (!confirm('are you sure you finish?')) {
                return 'Click "Cancel" to stay on this page';
            }
        };
    },
    methods: {
        add: function() {
            if (this.howManyCate < this.maxCate) {
                this.howManyCate = this.howManyCate + 1;
            } else {
                alert('Sorry, less than 5 categories');
                return;
            } 
        },
        capture: function() {
            html2canvas(document.querySelector("#app")).then(canvas => {
                let link = document.createElement('a');
                if (typeof link.download === 'string') {
                    link.href = canvas.toDataURL();
                    link.download = (new Date()).toString().split(' ').join('_') + '_result.png';
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);

                } else {
                    window.open(uri);
                }
            });
        }
    }
}
</script>

<style>
#app {
    font-family: 'Roboto', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}
</style>
