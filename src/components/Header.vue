<template>
<div class="row text-center" v-if="show = timeUp">
        <div class="col-sm-12 ">
            <div class="progress">
                <div class="progress-bar" role="progressbar" aria-valuenow="60" aria-valuemin="0" aria-valuemax ="100" :style="{width: secondSend + '%'}">
                </div>
            </div>
        </div>
    </div>
<!-- Or just put a timer! -->

  
</template>


<script>
export default {
    data () {
        return {
            show: true
        }
    },
    props: ["secondSend"],

    computed: {
        timeUp: function () {
            var qSend =  this.secondSend;
            if(qSend >= 100){
                this.$emit('timeDonReach', qSend)
                return false
            }
            else return true
        }
    }

}
</script>

<style>
.progress {
    width: 100px;
    margin-left: 40%
}

</style>