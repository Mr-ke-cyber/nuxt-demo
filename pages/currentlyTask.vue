<template>
  <div class="current-task">
    <h2 class="title">a summary list demo</h2>
    <h3 class="sub-title">2.Current doing in this week</h3>
    <ul class="task-list">
      <li v-for="(item,i) in taskLists" :key="i">
        <Input :class="item.isEdit?'':'no-edit'" clearable v-model="item.remark" :rows="1" maxlength="200"
               :show-word-limit="false" type="textarea" placeholder="Enter something..." style="width: 200px"/>
        <div class="status">Progress：</div>
        <Progress :percent="item.status" status="active" />
        <Button type="primary" @click="update(i)" size="small">Update</Button>
        <Button type="primary" @click="Save(i)" size="small">Save</Button>
      </li>
    </ul>
    <!--      <List>-->
    <!--        <ListItem v-for="(item,i) in taskLists" :key="i">-->
    <!--          <template slot="action">-->
    <!--            <Row>-->
    <!--              <Col span="21" offset="3">-->
    <!--&lt;!&ndash;                <Button type="info" @click="editTasks(i)" ghost style="margin-right:20px">Edit</Button>&ndash;&gt;-->
    <!--&lt;!&ndash;                <Button type="info" @click="saveTasks(i)" ghost>save</Button>&ndash;&gt;-->
    <!--              </Col>-->
    <!--            </Row>-->
    <!--          </template>-->
    <!--        </ListItem>-->
    <!--      </List>-->
  </div>
</template>

<script>
    export default {
        name: "currentlyTask",
        data() {
            return {
                taskLists: [
                    {
                        remark: 'currently doing task1',
                        isEdit: false,
                        status:30
                    }, {
                        remark: 'currently doing task2',
                        status:45,
                        isEdit: false
                    }, {
                        remark: 'currently doing task3',
                        status:85,
                        isEdit: false
                    }, {
                        remark: 'currently doing task4',
                        status:65,
                        isEdit: false
                    }
                ]
            }
        },
        methods:{
            update(i){
                this.taskLists[i].isEdit=true;
            },
            Save(i){
                this.taskLists[i].isEdit=false;
            }
        }
    }
</script>

<style scoped>
  .current-task {
    min-height: 100vh;
    padding: 0 20px;
  }

  .title {
    color: #C41230;
    text-align: center;
    font-size: 30px;
  }

  .sub-title {
    color: #2d8cf0;
    font-size: 18px;
    margin-top: 10px;
  }

  .task-list {
    list-style: none;
  }
  li{
    padding-bottom:10px;
    border-bottom:1px solid #00C58E;
  }
  /deep/ .ivu-btn{
    margin:15px 0 5px;
  }
  /deep/ .no-edit .ivu-input {
    border: none;
  }

  /deep/ .no-edit .ivu-input:focus {
    box-shadow: none;
  }

  /deep/ .ivu-input-type-textarea {
    margin-top: 10px;
  }
</style>
