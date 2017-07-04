<template>
    <div class="recharge">
    

    <div class="row">
    <table class="table table-bordered">
        <tr>
        <td>Xi - Interim moisture storage:</td>
           <td> <b-form-input type="number" v-model="Xi"></b-form-input></td>
        </tr>

         <tr>
           <td> Ei - Total depth of water removed by ET from the plant-root zone during day</td>
           <td> <b-form-input type="number" v-model="Ei"></b-form-input></td>
     </tr>
        <tr>
          <td>  Mm - Moisture-storage capcity of plant root zone</td>
            <td><b-form-input type="number" v-model="Mm"></b-form-input></td>
      </tr>
         <tr>
           <td> DR - Daily rate of direct recharge</td>
           <td> <b-form-input type="number" v-model="DR"></b-form-input></td>
     </tr>
    
         <tr>
           <td> Qi - Ground water recharge during day</td>
           <td> {{GroundWaterRecharge}}</td>
        </tr>
         <tr>
           <td> Mi - Moisture storage at the end of the current day</td>
          <td> {{MoistureStorageAtEndOfDay}}</td>
       </tr>
    </table>
    </div>

    <div class="row">
        <div class="col-sm">
        <p>If Xi - Ei <= Mm, then Qi = DR and Mi = Xi - Ei </p>
        </div>
        <div class="col-sm">
        <p>If Xi - Ei > Mm, then Qi = (Xi - Ei - Mm) + DR and Mi = Mm </p>
        </div>
        </div>
    </div>
</template>


<script>
export default {
    name: 'recharge',
    data() {
        return {
            /**
             * Xi - Interim moisture storage
             * Ei - total depth of water removed by ET from the plant-root zone during a day (L)
             * Mm - moisture-storage capacity of the plant-root zone (L)
             * Qi - groundwater recharge during the day (L)
             * Mi - moisture storage at the end of the current day i (L)
             * DR - daily rate of direct recharge (L) [a constant]
             **/

            Xi: 0,
            Ei: 0,
            Mm: 0,
            Qi: 0,
            DR: 0,
            Mi: 0
        }

    },

    computed: {
        GroundWaterRecharge: function () {
            if((parseFloat(this.Xi) - parseFloat(this.Ei)) <= parseFloat(this.Mm)){
                return parseFloat(this.DR);
            }
            else {
                return parseFloat(this.Xi) - parseFloat(this.Ei) - parseFloat(this.Mm) + parseFloat(this.DR);
            }
        },

        MoistureStorageAtEndOfDay: function (){
            if((parseFloat(this.Xi) - parseFloat(this.Ei)) <= parseFloat(this.Mm)){
                return parseFloat(this.Xi) - parseFloat(this.Ei);
            }
            else{
                return parseFloat(this.Mm);
            }
        }
    }
}
</script>


<style scoped>

</style>
