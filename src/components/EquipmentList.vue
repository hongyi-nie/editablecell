<template>
  <div class="equipment-container">
    <!-- 表格头部 -->
    <div class="table-header">
      <div class="header-item">作业对象</div>
      <div class="header-item">设备名称</div>
      <div class="header-item">设备ID</div>
      <div class="header-item">是否在线</div>
      <div class="header-item">更新时间</div>
      <div class="header-item">操作</div>
    </div>

    <!-- 设备列表 -->
    <div class="equipment-list">
      <div 
        v-for="(item, index) in equipmentData" 
        :key="index" 
        class="equipment-item"
      >
        <!-- 作业对象图片 -->
        <div class="equipment-image">
          <el-image
            :src="item.image"
            fit="cover"
            class="image"
            :preview-src-list="[item.image]"
          >
            <div slot="error" class="image-slot">
              <i class="el-icon-picture-outline"></i>
            </div>
          </el-image>
        </div>

        <!-- 设备名称 -->
        <div class="equipment-name">
          {{ item.name }}
        </div>

        <!-- 设备ID -->
        <div class="equipment-id">
          {{ item.id }}
        </div>

        <!-- 在线状态 -->
        <div class="equipment-status">
          <el-tag 
            :type="item.isOnline ? 'success' : 'danger'"
            size="small"
          >
            {{ item.isOnline ? '在线' : '离线' }}
          </el-tag>
        </div>

        <!-- 更新时间 -->
        <div class="equipment-time">
          {{ item.updateTime }}
        </div>

        <!-- 操作按钮 -->
        <div class="equipment-actions">
          <el-button 
            type="primary" 
            size="small"
            @click="viewDetails(item)"
          >
            详情
          </el-button>
        </div>
      </div>
    </div>

    <!-- 详情对话框 -->
    <el-dialog
      title="设备详情"
      :visible.sync="dialogVisible"
      width="50%"
    >
      <div v-if="selectedEquipment">
        <el-descriptions :column="2" border>
          <el-descriptions-item label="设备名称">
            {{ selectedEquipment.name }}
          </el-descriptions-item>
          <el-descriptions-item label="设备ID">
            {{ selectedEquipment.id }}
          </el-descriptions-item>
          <el-descriptions-item label="在线状态">
            <el-tag 
              :type="selectedEquipment.isOnline ? 'success' : 'danger'"
              size="small"
            >
              {{ selectedEquipment.isOnline ? '在线' : '离线' }}
            </el-tag>
          </el-descriptions-item>
          <el-descriptions-item label="更新时间">
            {{ selectedEquipment.updateTime }}
          </el-descriptions-item>
          <el-descriptions-item label="设备类型">
            {{ selectedEquipment.type || '未知' }}
          </el-descriptions-item>
          <el-descriptions-item label="位置信息">
            {{ selectedEquipment.location || '未知' }}
          </el-descriptions-item>
        </el-descriptions>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">关闭</el-button>
        <el-button type="primary" @click="dialogVisible = false">确定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'EquipmentList',
  data() {
    return {
      dialogVisible: false,
      selectedEquipment: null,
      equipmentData: [
        {
          image: 'https://via.placeholder.com/60x60/4CAF50/ffffff?text=设备1',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: false,
          updateTime: '2025-03-02',
          type: '监控设备',
          location: '东区A栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/2196F3/ffffff?text=设备2',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: true,
          updateTime: '2025-03-02',
          type: '传感器',
          location: '西区B栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/FF9800/ffffff?text=设备3',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: false,
          updateTime: '2025-03-02',
          type: '控制器',
          location: '南区C栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/9C27B0/ffffff?text=设备4',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: true,
          updateTime: '2025-03-02',
          type: '执行器',
          location: '北区D栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/F44336/ffffff?text=设备5',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: false,
          updateTime: '2025-03-02',
          type: '监控设备',
          location: '中心区E栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/607D8B/ffffff?text=设备6',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: true,
          updateTime: '2025-03-02',
          type: '传感器',
          location: '东区F栋'
        },
        {
          image: 'https://via.placeholder.com/60x60/795548/ffffff?text=设备7',
          name: '这是设备名称',
          id: 'sbjd4543234',
          isOnline: false,
          updateTime: '2025-03-02',
          type: '控制器',
          location: '西区G栋'
        }
      ]
    }
  },
  methods: {
    viewDetails(equipment) {
      this.selectedEquipment = equipment
      this.dialogVisible = true
    }
  }
}
</script>

<style scoped>
.equipment-container {
  background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
  min-height: 100vh;
  padding: 20px;
  font-family: 'Microsoft YaHei', sans-serif;
}

.table-header {
  display: grid;
  grid-template-columns: 80px 1fr 150px 100px 120px 80px;
  gap: 15px;
  padding: 15px 20px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  margin-bottom: 10px;
  backdrop-filter: blur(10px);
}

.header-item {
  color: #ffffff;
  font-weight: bold;
  font-size: 14px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

.equipment-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.equipment-item {
  display: grid;
  grid-template-columns: 80px 1fr 150px 100px 120px 80px;
  gap: 15px;
  padding: 15px 20px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
  align-items: center;
}

.equipment-item:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.equipment-image {
  display: flex;
  justify-content: center;
  align-items: center;
}

.image {
  width: 60px;
  height: 60px;
  border-radius: 8px;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.image-slot {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.1);
  color: #ffffff;
  font-size: 20px;
}

.equipment-name,
.equipment-id,
.equipment-time {
  color: #ffffff;
  font-size: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.equipment-status {
  display: flex;
  justify-content: center;
  align-items: center;
}

.equipment-actions {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .table-header,
  .equipment-item {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .header-item {
    display: none;
  }
  
  .equipment-item {
    display: flex;
    flex-direction: column;
    gap: 10px;
    align-items: center;
  }
  
  .equipment-image {
    order: 1;
  }
  
  .equipment-name {
    order: 2;
    font-weight: bold;
  }
  
  .equipment-id {
    order: 3;
  }
  
  .equipment-status {
    order: 4;
  }
  
  .equipment-time {
    order: 5;
  }
  
  .equipment-actions {
    order: 6;
  }
}

/* Element UI 组件样式覆盖 */
.el-dialog {
  background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
  border-radius: 15px;
}

.el-dialog__header {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px 15px 0 0;
  backdrop-filter: blur(10px);
}

.el-dialog__title {
  color: #ffffff;
  font-weight: bold;
}

.el-dialog__body {
  color: #ffffff;
}

.el-descriptions__label {
  color: #ffffff !important;
  font-weight: bold;
}

.el-descriptions__content {
  color: #ffffff !important;
}
</style>