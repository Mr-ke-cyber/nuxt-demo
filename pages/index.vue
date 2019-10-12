<template>
  <div class="container">
    <h2 class="title">a summary list demo</h2>
    <h3 class="sub-title">1.completed tasks last week</h3>
    <List item-layout="vertical">
      <ListItem v-for="(item,i) in taskLists" :key="i">
        <ListItemMeta
          avatar="https://dev-file.iviewui.com/userinfoPDvn9gKWYihR24SpgC319vXY8qniCqj4/avatar"
          description="Your assessment of completion of this task">
          <template slot="title">
            <Input :class="item.isEdit?'':'no-edit'" clearable v-model="item.name" placeholder="Enter your task title..."/>
            <Input :class="item.isEdit?'':'no-edit'" clearable v-model="item.remark" :rows="1" maxlength="200" :show-word-limit="false" type="textarea" placeholder="Enter something..." style="width: 200px" />
          </template>
        </ListItemMeta>
        <template slot="action">
          <Row style="margin-left:45px;">
            <Col span="24">
              <Rate show-text allow-half v-model="item.valueCustomText">
                <span style="color: #f5a623">{{ item.valueCustomText }}</span>
              </Rate>
            </Col>
          </Row>
        <Row>
          <Col span="21" offset="3">
            <Button type="info" @click="editTasks(i)" ghost style="margin-right:20px">Edit</Button>
            <Button type="info" @click="saveTasks(i)" ghost>save</Button>
          </Col>
        </Row>
        </template>
      </ListItem>
    </List>
    <div class="btn-wrapper">
      <Button type="primary" shape="circle" icon="ios-add-circle-outline" class="add-more-btn" @click="addMore">Add more</Button>
      <a href="/currentlyTask" class="current-doing-btn">Current doing  <Icon type="ios-arrow-forward" /></a>
    </div>
  </div>
</template>

<script>

    export default {
        components: {},
        data() {
            return {
                taskLists: [
                    {
                        name: 'this is task1 title',
                        remark:'this is remark of task1',
                        valueCustomText:3.0,
                        isEdit:false,
                    }, {
                        name: 'this is task2 title',
                        remark:'this is remark of task2',
                        valueCustomText:4.5,
                        isEdit:false
                    }
                ]
            }
        },
        methods: {
            editTasks(i) {
                this.taskLists[i].isEdit=true;
            },
            saveTasks(i){
                this.taskLists[i].isEdit=false;
            },
            addMore(){
                let newTask = {
                    name: '',
                    remark:'',
                    valueCustomText:0,
                    isEdit:true
                };
                this.taskLists.push(newTask);
            }
        }
    }
</script>

<style scoped>
  .container {
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
  /deep/ .no-edit .ivu-input{
    border:none;
  }
  /deep/ .no-edit .ivu-input:focus{
    box-shadow: none;
  }
  /deep/ .ivu-input-type-textarea{
    margin-top:20px;
  }
  /deep/ .ivu-list{
    border-bottom: 1px solid #e8eaec;
  }
  .btn-wrapper{
    padding:20px 0;
    display: flex;
    justify-content: space-around;
  }
  .current-doing-btn{
    color: #fff;
    background-color: #2d8cf0;
    display: inline-block;
    margin-bottom: 0;
    font-weight: 400;
    text-align: center;
    vertical-align: middle;
    touch-action: manipulation;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    height: 32px;
    line-height: 29px;
    padding: 0 15px;
    font-size: 14px;
    border-radius: 32px;
    transition: color .2s linear,background-color .2s linear,border .2s linear,box-shadow .2s linear;
  }
</style>
