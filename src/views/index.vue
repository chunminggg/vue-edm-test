<style scoped>
.index {
    width: 100%;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    text-align: center;
}

.formClass {
    margin-top: 10px
}

.formClass1 {
    padding: 10px;
    margin: 10px;
}

.setting {
    margin-left: 20px
}

.ivu-poptip-rel {
    width: 100%
}
</style>
<template>
    <div id="main">
    <router-link v-bind:to="'home'">Home</router-link>
        <Row>
            <Col span="4">
            <div class="drag">
                <Tabs value="name1">
                    <TabPane label="基本组件" name="basecomponent">
                        <draggable id="list1" :list="baseComList" class="dragArea" :options="{group:{name:'component', pull:'clone', put:false }}">
                            <div v-for="(element, index) in baseComList" :key="index">

                                <Button class="formClass" type="success" long> {{element.name}} </Button>
                            </div>
                        </draggable>
                    </TabPane>
                    <TabPane label="系统模块" name="systemcomponent">
                        <draggable id="list1" :list="sysComList" class="dragArea" :options="{group:{name:'component', pull:'clone', put:false }}">
                            <div v-for="(element, index) in sysComList" :key="index">

                                <Button class="formClass" type="success" long> {{element.name}}</Button>
                            </div>
                        </draggable>
                    </TabPane>
                </Tabs>

            </div>
            </Col>
            <Col span="12">
            <draggable id="list2" :list="acceptlist" class="dragArea" :options="{group:'component'}">
                <div v-for="(element, index)  in acceptlist" :key="index">
                    <div class="acceptComponent">
                        <Button class="formClass1" type="success" style="width:80%" @click="selectCompoent(index)"> {{element.name}}</Button>
                        <a @click="close(index)">操作</a>
                    </div>
                </div>
            </draggable>
            </Col>
            <Col span="8">
            <div class="setting">
                <Tabs value="name1">
                    <TabPane label="实验设置" name="name1">
                        <Input v-model="titleModel" placeholder="方案标题" style="width: 300px"></Input>
                        <Select class="formClass" v-model="sortSelected" style="width:200px">
                            <Option v-for="item in sortList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                        </Select>
                    </TabPane>
                    <TabPane label="模块设置" name="name2">
                        <div v-show="selecteModel.guid != undefined">
                            <Input v-model="componentTitle" placeholder="模块标题" style="width: 300px"></Input>
                        <Button class="formClass1" type="success"  > 资源引用</Button>
                        </div>
                        
                    </TabPane>
                </Tabs>

            </div>

            </Col>
        </Row>
    </div>
</template>
<script>
import draggable from 'vuedraggable'
export default {
    components: {
        draggable,

    },
    data() {
        return {
            titleModel: '',
            sortSelected: '1',
            sortList: [{
                value: '1',
                label: '化学生成'
            },
            {
                value: '2',
                label: '生物制药'
            },
            {
                value: '3',
                label: '分子模拟'
            }],
            baseComList: [{ name: "文本输入框", guid: '1' },
            { name: "单选框", guid: '2' },
            { name: "日期", guid: '3' }],
            acceptlist: [{ name: "文本输入框", guid: '1' }],
            sysComList: [{ name: '富文本编辑器', guid: '5' },
            { name: '电子表格', guid: '6' },
            { name: '信息表格', guid: '7' }
            ],
            visible: false,
            selecteModel: {},
            componentTitle: '',
        }
    },
    methods: {
        clone: function(el) {
            return {
                name: el.name + ' cloned'
            }
        },
        log: function(evt) {
            console.log(evt)
        },
        close(index) {
            this.visible = false;
            if (this.acceptlist.length > 1) {
                this.acceptlist.splice(index, 1)

            }
        },
        selectCompoent(index) {
            this.selecteModel = this.acceptlist[index]

        }
    }
};
</script>