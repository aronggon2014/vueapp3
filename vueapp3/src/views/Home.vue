<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-card color="#385F73" dark>
          <v-card-title>
            <div class="font-big">จำนวนลูกค้า</div>
          </v-card-title>

          <v-card-text>
            <div class="font-big">50คน</div>
          </v-card-text>

          <v-card-actions>
            <v-btn text>ข้อมูลลูกค้า</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col cols="4">
        <v-card color="#385F73" dark>
          <v-card-title>
            <div class="font-big">จำนวนสินค้า</div>
          </v-card-title>

          <v-card-text>
            <div class="font-big">20ชิ้น</div>
          </v-card-text>

          <v-card-actions>
            <v-btn text>ข้อมูลสินค้าค้า</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>

      <v-col cols="4">
        <v-card color="#385F73" dark>
          <v-card-title>
            <div class="font-big">จำนวนรายงาน</div>
          </v-card-title>

          <v-card-text>
            <div class="font-big">16รายการ</div>
          </v-card-text>

          <v-card-actions>
            <v-btn text>ข้อมูลรายงาน</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <!-- <อันใหม่> -->
    <v-row>
      <v-col cols="12">
        <v-card class="mx-auto text-center" color="red" dark>
          <v-card-text>
            <v-sheet color="rgba(0, 0, 0,  .12)">
              <v-sparkline
                :value="value"
                color="rgba(4, 47, 89, 1 .7)"
                height="100"
                padding="24"
                stroke-linecap="round"
                smooth
                line-width="4"
              >
                <template v-slot:label="item">{{ item.value }} บ.</template>
              </v-sparkline>
            </v-sheet>
          </v-card-text>

          <v-card-text>
            <div class="font-big">รายงานการขาย</div>
          </v-card-text>

          <v-divider></v-divider>

          <!-- <v-card-actions class="justify-center"> -->
          <!-- <v-btn block text>รายงานการขาย</v-btn> -->
          <!-- </v-card-actions> -->
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data() {
    return {
      value: [323, 446, 675, 150, 590, 610, 800]
    };
  }
};
</script>

<style scope>
.font-big {
  font-size: 30px;
}
</style>