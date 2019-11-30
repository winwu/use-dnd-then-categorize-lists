<template>
    <div class="dndview">
        <div class="badge badge-primary">{{ msg }}</div>
        <div class="mb-1">
            <strong>
                Please use drag and drop these item into category:
            </strong>
        </div>
        <div class="source-box">
            <div class="source-title">Types:</div>
            <div id="source-g" class="row">
                <div class="col-12">
                    <draggable :list="sources" group="same" @change="log">
                        <div class="d-inline-block sample-item" :style="{ background: element.background }" :key="index" v-for="(element, index) in sources" >
                            <div>{{ element.name }}</div>
                        </div>
                    </draggable>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-3" v-for="(g, index) in groups" :key="index" :data-idx="index">
                <div class="category-box">
                    <div>
                        <div class="badge badge-default">Group {{index+1}}</div>
                        <div class="form-inline">
                            <div class="input-group input-group-sm mb-2 mr-sm-2">
                                <div class="input-group-prepend">
                                    <div class="input-group-text">naming</div>
                                </div>
                                <input type="text" class="form-control form-control-sm" :name="'group_' + index + '_name'" placeholder="category name">
                            </div>
                        </div>
                    </div>
                    <draggable class="list-group" :list="g.lists" group="same" @change="log">
                        <div class="list-group-item" :key="index2" :style="{ background: element.background }" v-for="(element, index2) in g.lists">
                            {{ element.name }}
                        </div>
                    </draggable>
                </div>
            </div>
            <div class="col-3">
                <button class="btn btn-outline-primary" @click.prevent.stop="addGroup">Add Group</button>
            </div>
        </div>
    </div>
</template>

<script>
import draggable from 'vuedraggable'
import { mkdir } from 'fs';

export default {
    name: 'DndView',
    props: {
        msg: String
    },
    components: {
        draggable
    },
    data() {
        return {
            sources: [
                {
                    id: '1',
                    name: 'First category',
                    background: 'pink',
                    video_name: 'spinner'
                },
                {
                    id: '1',
                    name: 'Second category',
                    background: 'red',
                    video_name: 'progressspin'
                },
                {
                    id: '3',
                    name: 'Third category',
                    background: 'orange',
                    video_name: 'progressbar'
                }
            ],
            groups: [
                {
                    lists: []
                },
                {
                    lists: []
                }
            ]
        };
    },
    methods: {
        addGroup: function() {
            this.groups.push({
                name: '',
                lists: []
            })
        },
        log: function(evt) {
            window.console.log(evt);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.dndview {
    text-align: left;
}
.sample-item {
    border: 1px solid #e9e9e9;
    margin: 15px 0px;
    width: 276px;
    padding: 5px;
    box-sizing: border-box;
    cursor: pointer;
}
.category-box {
    margin-bottom: 15px;
    border: 3px solid #dedede;
    border-radius: 2px;
    padding: 10px;
    background: #f8f8f8;
}
.category-box .list-group {
    min-height: 250px;
    background: #fff;
    border: 2px solid #bfbfbf;
    position: relative;
}

.source-box {
    background: #fff;
    box-shadow: 2px 2px 10px #d8d8d8;
    padding: 24px 10px 10px 10px;
    margin: 10px auto 30px auto;
    border-radius: 4px;
    position: relative;
}
.source-box  .source-title {
    position: absolute;
    left: 0;
    top: 0;
    padding: 1px 15px;
    font-size: 14px;
    color: #575757;
    font-weight: bold;
    background: #eee;
    border-radius: 0 0 4px 0;
}
</style>
