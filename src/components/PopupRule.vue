<template>
    <div class="wrapper-popup" v-bind:class = "getClassPopup">
        <div class="rule">
            <h3>Luật Chơi</h3>
            <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. 
            Ipsam velit reiciendis nulla rerum aliquam amet, 
            rem recusandae ipsum inventore ducimus, 
            pariatur reprehenderit unde, voluptas explicabo culpa
            in a numquam laboriosam!</p>
            <button v-on:click = "confim" class="confim">Đã Hiểu</button>
        </div>
    </div>
</template>

<script>
export default {
    name:'popup-rule',
    data(){
        return {

        }
    },
    props:{
        isOpenpopup: { type : Boolean, default : false }
    },
    methods:{
        confim(){
            this.$emit('handelConfim');
        }
    },
    computed:{
        getClassPopup: function(){
            return {
                'open-popup' : this.isOpenpopup
            }
        }
    }
}
</script>

<style>
    .wrapper-popup{
        position: fixed;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        background-color: rgba(0, 0,0, 0.4);
        opacity: 0;
        visibility: hidden;
        transition: all .3s ease;
    }
    .wrapper-popup.open-popup{
        opacity: 1;
        visibility: visible;
        transition: all .3s ease;
    }
    .rule{
        font-family: Arial;
        width: 350px;
        padding: 20px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(1.3);
        background: #fff;
        position: absolute;
        transition: all .3s ease;
    }
    .rule h3{
        margin-bottom: 30px;
    }
    .confim{
        cursor: pointer;
        background-color: #fff;
        padding: 8px 15px;
        margin-top: 30px;
        border: 2px solid #f333;
        transition: all .3s ease;
    }
    .confim:hover{
        background-color: black;
        color: #fff;
    }
</style>