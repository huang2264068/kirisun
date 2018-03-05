<template>
    <el-container>
        <el-header>
            <el-row :gutter="20" class="nav" >
                <el-col :lg="4" :sm="4" :xs="12" :offset="2">
                    <div class="grid-content bg-purple with">
                        <!-- <div class="logoImg"></div> -->
                        <img class="logoImg" src="../../assets/logo/login_kelixun_us.png">
                    </div>
                </el-col>
                <el-col :lg="4" :sm="4" :offset="12" class="holp hidden-xs-only holp" >
                    <div class="grid-content bg-purple">帮助中心</div>
                </el-col>
            </el-row>

        </el-header>
        <el-main class="bodyLg">
            <el-row :gutter="10">
                <el-col :lg="12" :offset="2" class="hidden-md-and-down">
                    <div class="grid-content bg-purple with">
                        <el-row :gutter="10">
                            <el-col :lg="20" >
                                <p class="title">PoC  集群系统管理平台</p>
                            </el-col>
                        </el-row>
                        <el-row :gutter="10">
                            <el-col :lg="20" class="hidden-xs-only">
                                <img  class="mainImg" src="../../assets/loginbg.png">
                            </el-col>
                        </el-row>
                    </div>
                </el-col>
                <el-col :lg="9" :md="12" :sm="4" :offset="1" class="hidden-md-and-down">
                    <div class="grid-content bg-purple">
                        <div class="loginLg"  style="width:380px">
                            <el-form :model="ruleForm2" status-icon :rules="rules2" ref="ruleForm2" label-width="15%" class="demo-ruleForm">
                                <h1 class="loginTitle">{{loginTitle}}</h1>
                                <el-form-item prop="uname" style="width:85%">
                                    <el-input type="text" v-model="ruleForm2.uname" :placeholder="unameInput" auto-complete="off"></el-input>
                                </el-form-item>
                                <el-form-item prop="checkPass" style="width:85%">
                                    <el-input type="password" v-model="ruleForm2.pass" :placeholder="upwdInput" auto-complete="off"></el-input>
                                </el-form-item>
                                <el-form-item prop="checkInput" >
                                    <div class="movebox" >
                                        <div class="movego"></div>
                                        <div class="txt" id="txt">拖动滑块验证</div>
                                        <div class="move moveBefore" v-move></div>
                                    </div>
                                </el-form-item>
                                <el-form-item prop="checkInput" >
                                    
                                </el-form-item>
                                <el-form-item style="width:85%">
                                    <el-button type="success" @click="submitForm('ruleForm2')" style="width:100%">登录</el-button>
                                </el-form-item>
                            </el-form>
                        </div>
                    </div>
                </el-col>
            </el-row>
            <!-- <el-row :gutter="10">
                <el-col :lg="12" :md="12" :sm="6"  :offset="2">
                    <div class="grid-content bg-purple with">
                        <el-row :gutter="10">
                            <el-col :lg="20" :md="24" :sm="20"  >
                                <p class="title">PoC  集群系统管理平台</p>
                            </el-col>
                        </el-row>
                        <el-row :gutter="10">
                            <el-col :lg="20" :md="24" :sm="20" class="hidden-xs-only">
                               
                                <img  class="mainImg" src="../../assets/loginbg.png">
                            </el-col>
                        </el-row>
                    </div>
                </el-col>
                <el-col :lg="9" :md="12" :sm="4" :offset="1" class="hidden-md-and-down">
                    <div class="grid-content bg-purple">
                         <el-row>
                            <el-col :lg="20" :md="22">
                                <div class="login">

                                </div>
                            </el-col>
                        </el-row>
                    </div>
                </el-col>
            </el-row> -->
        </el-main>
        <el-footer class="foot">Footer</el-footer>
    </el-container>
</template>

<script>
// import loginFrom from '@/components/login/loginFrom'
export default {
  data() {
      var validateuname = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请输入用户名'));
        } else {
          callback();
        }
      };
      var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请输入密码'));
        } else {
          callback();
        }
      };
      
      return {
          loginTitle:'用户登录',
          unameInput:'请输入用户名',
          upwdInput:'请输入密码',
        ruleForm2: {
          uname: '',
          pass: ''
        },
        rules2: {
          uname: [
            { validator: validateuname, trigger: 'blur' }
          ],
          checkPass: [
            { validator: validatePass, trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    },
    directives: {
        
        move(el) {
            el.onmousedown = function(e) {
                var X = e.clientX - el.offsetLeft
                document.onmousemove = function(e) {
                    var endx = e.clientX - X
                    el.className = 'move moveBefore'
                    el.style.left = endx + 'px'
                    // console.log(el.parentNode.children[0])
                    var width = $('.movebox').width() - $('.move').width()
                    el.parentNode.children[0].style.width = endx + 'px'
                    el.parentNode.children[1].innerHTML = '拖动滑块验证'
                    //临界值小于
                    if (endx <= 0) {
                        el.style.left = 0 + 'px'
                        el.parentNode.children[0].style.width = 0 + 'px'
                        //$('.movego').width(0)
                    }
                    //临界值大于
                    // console.log(el.style.left)
                    if (parseInt(el.style.left) >= width) {
                        el.style.left = width + 'px'
                        el.parentNode.children[0].style.width = width + 'px'
                        el.parentNode.children[1].innerHTML = '验证通过'
                        el.className = 'move moveSuccess'
                        el.onmousedown = null
                    }
            }
        }
        document.onmouseup = function() {
            document.onmousemove = null
        }
    }
  }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .with{
        width: 100%;
        height: 100%;
        /* line-height: 400%; */
    }
    .logoImg{
        display: block;
        width: 100%;
        height: 100%;
        margin-top: 10%;
        /* background:url("../../assets/logo/login_kelixun_us.png") no-repeat; */
    }
    .holp{
        height:100%;
        line-height: 400%;
        font-size: 1.4rem;
        font-weight: bold;
    }
    .mainImg{
        width: 100%;
        height:100%;
        /* background-image: url("../../assets/loginbg.png") */
    }
    .bodyLg{
        margin-top: 2%;
        background-color: rgb(21, 120, 174);
        padding-top: 3%;
        padding-bottom: 4%;
    }
    p{
        color: #fff;
        font-size: 1.4em;
        width: 100%;
    }
    .loginLg{
        width: 100%;
        height: 25rem;
        border: 2px solid #fff;
        border-radius: 15px;
        margin-top: 10%;
    }
    .foot{
        line-height: 60px
    }
    .loginTitle{
        color: #fff;
        font-size: 2rem;
    }
    .movebox{
        position: relative;
        margin-left:-3%; 
        background-color: #e8e8e8;
        height: 34px;
        width: 85%;
        line-height: 34px;
        text-align: center;
    }
  .txt{
        position: absolute;
        top: 0px;
        width: 100%;
        -moz-user-select: none;
        -webkit-user-select: none;
        user-select: none;
        -o-user-select: none;
        -ms-user-select: none;
    }
  .movego{
        background-color: #7ac23c;
        height: 34px;
        width: 0px;
    }
   .move{
        position: absolute;
        top: 0px;
        left: 0px;
        width: 40px;
        height: 34px;
        border: 1px solid #ccc;
        cursor: move;
   }
   .moveBefore{
     background: #fff url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAA3hpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNS1jMDIxIDc5LjE1NTc3MiwgMjAxNC8wMS8xMy0xOTo0NDowMCAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtcE1NOk9yaWdpbmFsRG9jdW1lbnRJRD0ieG1wLmRpZDo0ZDhlNWY5My05NmI0LTRlNWQtOGFjYi03ZTY4OGYyMTU2ZTYiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6NTEyNTVEMURGMkVFMTFFNEI5NDBCMjQ2M0ExMDQ1OUYiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6NTEyNTVEMUNGMkVFMTFFNEI5NDBCMjQ2M0ExMDQ1OUYiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTQgKE1hY2ludG9zaCkiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDo2MTc5NzNmZS02OTQxLTQyOTYtYTIwNi02NDI2YTNkOWU5YmUiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6NGQ4ZTVmOTMtOTZiNC00ZTVkLThhY2ItN2U2ODhmMjE1NmU2Ii8+IDwvcmRmOkRlc2NyaXB0aW9uPiA8L3JkZjpSREY+IDwveDp4bXBtZXRhPiA8P3hwYWNrZXQgZW5kPSJyIj8+YiRG4AAAALFJREFUeNpi/P//PwMlgImBQkA9A+bOnfsIiBOxKcInh+yCaCDuByoswaIOpxwjciACFegBqZ1AvBSIS5OTk/8TkmNEjwWgQiUgtQuIjwAxUF3yX3xyGIEIFLwHpKyAWB+I1xGSwxULIGf9A7mQkBwTlhBXAFLHgPgqEAcTkmNCU6AL9d8WII4HOvk3ITkWJAXWUMlOoGQHmsE45ViQ2KuBuASoYC4Wf+OUYxz6mQkgwAAN9mIrUReCXgAAAABJRU5ErkJggg==") no-repeat center;
 
     
   }
   .moveSuccess{
      background: #fff url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAA3hpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNS1jMDIxIDc5LjE1NTc3MiwgMjAxNC8wMS8xMy0xOTo0NDowMCAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtcE1NOk9yaWdpbmFsRG9jdW1lbnRJRD0ieG1wLmRpZDo0ZDhlNWY5My05NmI0LTRlNWQtOGFjYi03ZTY4OGYyMTU2ZTYiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6NDlBRDI3NjVGMkQ2MTFFNEI5NDBCMjQ2M0ExMDQ1OUYiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6NDlBRDI3NjRGMkQ2MTFFNEI5NDBCMjQ2M0ExMDQ1OUYiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTQgKE1hY2ludG9zaCkiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDphNWEzMWNhMC1hYmViLTQxNWEtYTEwZS04Y2U5NzRlN2Q4YTEiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6NGQ4ZTVmOTMtOTZiNC00ZTVkLThhY2ItN2U2ODhmMjE1NmU2Ii8+IDwvcmRmOkRlc2NyaXB0aW9uPiA8L3JkZjpSREY+IDwveDp4bXBtZXRhPiA8P3hwYWNrZXQgZW5kPSJyIj8+k+sHwwAAASZJREFUeNpi/P//PwMyKD8uZw+kUoDYEYgloMIvgHg/EM/ptHx0EFk9I8wAoEZ+IDUPiIMY8IN1QJwENOgj3ACo5gNAbMBAHLgAxA4gQ5igAnNJ0MwAVTsX7IKyY7L2UNuJAf+AmAmJ78AEDTBiwGYg5gbifCSxFCZoaBMCy4A4GOjnH0D6DpK4IxNSVIHAfSDOAeLraJrjgJp/AwPbHMhejiQnwYRmUzNQ4VQgDQqXK0ia/0I17wJiPmQNTNBEAgMlQIWiQA2vgWw7QppBekGxsAjIiEUSBNnsBDWEAY9mEFgMMgBk00E0iZtA7AHEctDQ58MRuA6wlLgGFMoMpIG1QFeGwAIxGZo8GUhIysmwQGSAZgwHaEZhICIzOaBkJkqyM0CAAQDGx279Jf50AAAAAABJRU5ErkJggg==") no-repeat center;
 
     
   }
  
</style>
