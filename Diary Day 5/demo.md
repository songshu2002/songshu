<div id="app">
    <input type="text" v-model="inputvalue">
    <button @click="tijiao">
        提交
    </button>
    <ul>
        <li v-for="item in list">{{item}}</li>
    </ul>
</div>

<script>
    var app = new Vue({
        el:'#app',
        data:{
            inputvalue:'',
            list:[]
        },
        methods:{
            tijiao:function (){
                this.list.push(this.inputvalue);
                this.inputvalue = '';
            }


        }
    })
</script>



