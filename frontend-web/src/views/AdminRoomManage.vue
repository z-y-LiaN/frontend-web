<template>
  <!--  设置机房机位状态页面、新增机房？-->
  <el-select v-model="selectedRoomID" placeholder="请选择机房" @change="selectRoom()">
    <el-option v-for="room in rooms" :key="room.value" :label="room.label" :value="room.label">
    </el-option>
  </el-select>
  <el-card class="box-card">

    <el-row :gutter="0">
      <el-col :span="6" :offset="0">
        <div class="grid-content bg-purple">
          <el-tag style="display: block;">当前机房：{{ roomInfo.roomID }}</el-tag>
          <el-tag style="display: block;">机房性质：{{ roomInfo.roomKind }}</el-tag>
          <el-tag style="display: block;">当前状态：{{ roomInfo.roomStatus }}</el-tag>
        </div>
      </el-col>
      <el-col :span="6" :offset="4">
        <div class="grid-content bg-purple">
          <el-button>启用/禁用机房</el-button>
        </div>
      </el-col>
      <el-col :span="3" :offset="20">
        <div class="grid-content bg-purple">
          <el-row>
            <el-button type="success" size="mini"></el-button>
            启用中
          </el-row>
          <el-row>
            <el-button type="danger" size="mini"></el-button>
            禁用中
          </el-row>
        </div>
      </el-col>
    </el-row>

  </el-card>
  <el-empty :image-size="200" v-if="isEmpty()"></el-empty>
  <el-card class="box-card" v-if="seatsVisible">
    <el-row :gutter="20" v-for="itemRow of deviceData" :key="itemRow" :span="5" size="mini" :offset=item*2>
      <el-card>
        <el-button :type="deviceStatusColor(device.deviceStatus)" v-for="device of itemRow " :key="device">[
          {{ device.deviceRow }} , {{ device.deviceCol }} ]
        </el-button>
      </el-card>
    </el-row>
  </el-card>
  <router-view></router-view>
</template>

<script>
export default {
  name: "AdminRoomManage",
  data() {
    return {
      seatsVisible: false,
      rooms: [],
      selectedRoomID: '',
      roomInfo: {},
      deviceStatusColor: function (val) {
        if (val == '可用') {
          return 'success'
        } else if (val == '禁用') {
          return 'danger'
        } else if (val == '禁用') {
          return 'red'
        } else if (val == '延后处理') {
          return 'danger'
        } else {
          return 'green'
        }
      },
      deviceData: '',
    }
  },
  methods: {
    isEmpty(){
      if(this.selectedRoomID==""||this.selectedRoomID==null)
        return true
      else
        return false
    },

    selectRoom(e) {
      if (this.selectedRoomID != '' && this.selectedRoomID != null) {
        //将selectedRoomID传给后端，后端返回该room的信息:roomInfo;和room拥有的所有的device信息:deviceData
        this.roomInfo = {
          roomID: '1001',
          roomName: '机房1001',
          roomKind: '软件',
          roomRow: 8, //假设8行7列
          roomCol: 7,
          roomStatus: '已启用'
        }
        this.deviceData = [
          [{
            roomID: '1001',
            deviceRow: 1,
            deviceCol: 1,
            deviceStatus: '可用'
          },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 2,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 3,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 4,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 5,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 6,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 7,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 8,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 1,
              deviceCol: 9,
              deviceStatus: '可用'
            },
          ],
          [{
            roomID: '1001',
            deviceRow: 2,
            deviceCol: 1,
            deviceStatus: '可用'
          },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 2,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 3,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 4,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 5,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 6,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 7,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 8,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 2,
              deviceCol: 9,
              deviceStatus: '可用'
            },
          ],
          [{
            roomID: '1001',
            deviceRow: 3,
            deviceCol: 1,
            deviceStatus: '可用'
          },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 2,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 3,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 4,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 5,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 6,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 7,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 3,
              deviceCol: 8,
              deviceStatus: '可用'
            }
          ],
          [{
            roomID: '1001',
            deviceRow: 4,
            deviceCol: 1,
            deviceStatus: '可用'
          },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 2,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 3,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 4,
              deviceStatus: '禁用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 5,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 6,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 7,
              deviceStatus: '可用'
            },
            {
              roomID: '1001',
              deviceRow: 4,
              deviceCol: 8,
              deviceStatus: '可用'
            }
          ],
        ]
      }
      this.seatsVisible = true;
      console.log(this.selectedRoomID)
    }
  },
  created() {
    //获取后端的所有room的信息
    this.rooms = [{
      value: '1001',
      label: '机房1001'
    }, {
      value: '1002',
      label: '机房1002'
    }, {
      value: '1003',
      label: '机房1003'
    }, {
      value: '1004',
      label: '机房1004'
    }, {
      value: '1005',
      label: '机房1005'
    }]
  }
}
</script>

<style scoped>
.el-dropdown {
  vertical-align: top;
}

.el-dropdown + .el-dropdown {
  margin-left: 15px;
}

.el-icon-arrow-down {
  font-size: 12px;
}
</style>
