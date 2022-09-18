<template>
    <!--illegal auth alert-->
    <div id="ErrorAlert" class="alert alert-danger alert-dismissible" style="padding: 2%; z-index: 5;width:60%; max-width: 60%; left: 20%; font-size: 2.5vw; display: none; top: 0; position: fixed; border-radius: 2em; margin-top: 4%;">
        <strong>Error!</strong>
        <div style="font-size: 2vw;">
            <span id="ErrorAlertMsg"></span><br>
            Expired or Illegal Authentication,<br> Please Log-in first.<br>
            5'Sec Later Will Direct To Log-in Page.
        </div>
    </div>
    <!--log out check message-->
    <div id="LogOutWarn" class="alert alert-warning alert-dismissible" style="padding: 2%; z-index: 5; width: 60%; height: fit-content; left: 20%; font-size: 3vw; top: 20%; position: fixed; border-radius: 2em; display: none">
        <strong>Warning!</strong>
        <div style="font-size: 2.5vw; width: 100%;">
            <br>
            You're now log out,
            <br>
            Really wanna Log out ??
            <div style="display: inline-block; width: 100%; margin-top: 6%;">
                <button class="btn btn-info btn-logout" @click="LogOut();" style="margin-right:20%;">Yes</button><button class="btn btn-danger btn-logout" @click="closeAlert();">No</button>
            </div>
        </div>
    </div>
    <div id="all">
        <!--Title bar-->
        <div class="TitleBar">
            <span class="En"><strong>Vue 3.0 with .Net Core 6 API - CRUD</strong></span>
        </div>

        <!--log out button-->
        <button class="LogOut" @click="showCheckAlert();" title="Log Out"><span class="glyphicon">&#xe163;</span></button>

        <img alt="logo" src="@/assets/logo-1.png">
        <!--loading spinner-->
        <div class="spinnerGrop" id="spinnerGrop">
            <div class="spinner-grow text-primary BigSpinner"></div>
            <div class="spinner-grow text-success BigSpinner"></div>
            <div class="spinner-grow text-warning BigSpinner"></div>
            <div class="spinner-grow text-danger BigSpinner"></div>
        </div>
        <!--Background Cloud animation-->
        <div class="BackgroundCloud">
            <div class="clouds">
                <img src="@/assets/Cloud-1.png">
                <img src="@/assets/Cloud-3.png">
                <img src="@/assets/Cloud-2.png">
                <img src="@/assets/Cloud-3.png">
                <img src="@/assets/Cloud-1.png">
                <img src="@/assets/Cloud-3.png">
                <img src="@/assets/Cloud-2.png">
                <img src="@/assets/Cloud-1.png">
                <img src="@/assets/Cloud-3.png">
                <img src="@/assets/Cloud-2.png">
            </div>
        </div>
        <!--user info、icon-->
        <div class="UserInfo">
            <span class="glyphicon glyphicon-user" style="margin-bottom: 2%; font-size: 2vw;"><span id="UserAccount" class="Ch" style="font-size: 2vw;"></span></span>
            <p>
                <span class="Ch" style="font-size: 1.5vw;">Permissive Action : </span>&emsp;
                <span class="label label-primary Ch" style="margin: 1%; width: auto; font-size: 1.1vw; height: fit-content; padding: 0.8%; border-radius: 5em; ">Get</span>
                <span id="PostTag" class="label label-success Ch" style="margin: 1%; width: auto; font-size: 1.1vw; height: fit-content; padding: 1.2%; border-radius: 5em; display: none; ">Post</span>
                <span id="PutTag" class="label label-warning Ch" style="margin: 1%; width: auto; font-size: 1.1vw; height: fit-content; padding: 1.2%; border-radius: 5em; display: none; ">Put</span>
                <span id="DeleteTag" class="label label-danger Ch" style="margin: 1%; width: auto; font-size: 1.1vw; height: fit-content; padding: 1.2%; border-radius: 5em; display: none; ">Delete</span>
            </p>
        </div>


        <!--crud contain-->
        <div class="container" style="margin-bottom: 2%;">
            <!--Get All-->
            <div class="accordion">
                <input type="checkbox" id="GetAll">
                <div class="ActionText" style="background: #4682B4;">
                    <label for="GetAll">Get&emsp;<span class="URLText" style="border: 2px inset #4682B4;">/api/DataBase</span></label>
                </div>
                <div class="p">
                    <hr /><span class="Ch Thead"><strong>Parameters</strong></span><hr />
                    <div class="Para">
                        <div class="Tbody">No parameter.</div>
                        <button class="btn btn-primary ExecuteBtn" @click="InitDiv('GetAll_ErrorMsg','GetAll_Response'); GetAll();">Execute</button>
                    </div>

                    <hr /><span class="Ch Thead"><strong>Response</strong></span><hr />
                    <div class="Resp">
                        <pre id="GetAll_Response" class="RespMsg"></pre><!--successful-->
                        <div id="GetAll_ErrorMsg" class="ErrorMsg"></div><!--error msg-->
                    </div>
                </div>
            </div>
            <!--Post-->
            <div class="accordion" id="PostBar" style="display: none">
                <input type="checkbox" id="Post">
                <div class="ActionText" style="background: #46B482; ">
                    <label for="Post">Post&emsp;<span class="URLText" style="border: 2px inset #46B482;">/api/DataBase</span></label>
                </div>
                <div class="p">
                    <hr /><span class="Ch Thead"><strong>Parameters</strong></span><hr />
                    <div class="Para">
                        <div class="Tbody input-group">
                            <span class="input-group-addon En ParaLabel"><strong>Data : </strong></span>
                            <input type="text" class="form-control ParaInput" id="PostData" placeholder="Data type is string">
                        </div>
                        <button class="btn btn-primary ExecuteBtn" @click="InitDiv('Post_ErrorMsg','Post_Response'); Post();">Execute</button>
                    </div>

                    <hr /><span class="Ch Thead"><strong>Response</strong></span><hr />
                    <div class="Resp">
                        <pre id="Post_Response" class="RespMsg"></pre><!--successful-->
                        <div id="Post_ErrorMsg" class="ErrorMsg"></div><!--error msg-->
                    </div>
                </div>
            </div>
            <!--Get Data By Id-->
            <div class="accordion">
                <input type="checkbox" id="Get">
                <div class="ActionText" style="background: #4682B4;">
                    <label for="Get">Get&emsp;<span class="URLText" style="border: 2px inset #4682B4;">/api/DataBase/{Id}</span></label>
                </div>
                <div class="p">
                    <hr /><span class="Ch Thead"><strong>Parameters</strong></span><hr />
                    <div class="Para">
                        <div class="Tbody input-group">
                            <span class="input-group-addon En ParaLabel"><strong>Id : </strong></span>
                            <input type="text" class="form-control ParaInput" id="GetId" placeholder="Id type is byte">
                        </div>
                        <button class="btn btn-primary ExecuteBtn" @click="InitDiv('Get_Response','Get_ErrorMsg'); Get();">Execute</button>
                    </div>

                    <hr /><span class="Ch Thead"><strong>Response</strong></span><hr />
                    <div class="Resp">
                        <pre id="Get_Response" class="RespMsg"></pre><!--successful-->
                        <div id="Get_ErrorMsg" class="ErrorMsg"></div><!--error msg-->
                    </div>
                </div>
            </div>
            <!--Update Data By Id-->
            <div class="accordion" id="PutBar" style="display: none">
                <input type="checkbox" id="Put">
                <div class="ActionText" style="background: #E69138;">
                    <label for="Put">Put&emsp;<span class="URLText" style="border: 2px inset #E69138;">/api/DataBase/{Id}</span></label>
                </div>
                <div class="p">
                    <hr /><span class="Ch Thead"><strong>Parameters</strong></span><hr />
                    <div class="Para">
                        <div class="Tbody input-group">
                            <span class="input-group-addon En ParaLabel"><strong>Id : </strong></span>
                            <input type="text" class="form-control ParaInput" id="PutId" placeholder="Id type is byte">
                            <span class="input-group-addon En ParaLabel"><strong>Data : </strong></span>
                            <input type="text" class="form-control ParaInput" id="PutData" placeholder="Data type is string">
                        </div>
                        <button class="btn btn-primary ExecuteBtn" @click="InitDiv('Put_ErrorMsg','Put_Response'); Put();">Execute</button>
                    </div>

                    <hr /><span class="Ch Thead"><strong>Response</strong></span><hr />
                    <div class="Resp">
                        <pre id="Put_Response" class="RespMsg"></pre><!--successful-->
                        <div id="Put_ErrorMsg" class="ErrorMsg"></div><!--error msg-->
                    </div>
                </div>
            </div>
            <!--Delete Data By Id-->
            <div class="accordion" id="DeleteBar" style="display: none">
                <input type="checkbox" id="Delete">
                <div class="ActionText" style="background: #D63333;">
                    <label for="Delete">Delete&emsp;<span class="URLText" style="border: 2px inset #D63333;">/api/DataBase/{Id}</span></label>
                </div>
                <div class="p">
                    <hr /><span class="Ch Thead"><strong>Parameters</strong></span><hr />
                    <div class="Para">
                        <div class="Tbody input-group">
                            <span class="input-group-addon En ParaLabel"><strong>Id : </strong></span>
                            <input type="text" class="form-control ParaInput" id="DeleteId" placeholder="Id type is byte">
                        </div>
                        <button class="btn btn-primary ExecuteBtn" @click="InitDiv('Delete_Response','Delete_ErrorMsg'); Delete();">Execute</button>
                    </div>

                    <hr /><span class="Ch Thead"><strong>Response</strong></span><hr />
                    <div class="Resp">
                        <pre id="Delete_Response" class="RespMsg"></pre><!--successful-->
                        <div id="Delete_ErrorMsg" class="ErrorMsg"></div><!--error msg-->
                    </div>
                </div>
            </div>
        </div>
        <!--參考資料區塊-->
        <div class="Reference">
            <h2><span class="En"><strong>Reference</strong></span></h2>
            <ul>
                <li><a href="https://www.youtube.com/watch?v=GdWrYfDfqRE&list=PL4cUxeGkcC9gCtAuEdXTjNVE5bbMFo5OD&index=5&ab_channel=TheNetNinj" target="_blank" rel="noopener">Vue & Typescript tutorial</a></li>
                <li><a href="https://medium.com/web-design-zone/vue-js-%E4%BD%BF%E7%94%A8vue-cli%E5%AE%89%E8%A3%9D-vue3-f54d05ef348e" target="_blank" rel="noopener">Vue CLI install Vue 3.0</a></li>
                <li><a href="https://vuejs.org/guide/typescript/overview.html#ide-support" target="_blank" rel="noopener">Vue with Typescript</a></li>
            </ul>
            <ul>
                <li><a href="https://blog.logrocket.com/axios-vs-fetch-best-http-requests/" target="_blank" rel="noopener">Reason to use axios</a></li>
                <li><a href="https://kalacloud.com/blog/vue3-typescript-axios/" target="_blank" rel="noopener">Vue with axios</a></li>
            </ul>
            <ul>
                <li><a href="https://www.w3schools.com/bootstrap4/tryit.asp?filename=trybs_spinners_grow&stacked=h" target="_blank" rel="noopener">bootstrap</a></li>
                <li><a href="https://freefrontend.com/css-accordions/" target="_blank" rel="noopener">css accordion</a></li>
            </ul>

        </div>
        <!--底部時間-->
        <div class="FixedBar">
            <span id="Timer" class="En"><strong>{{Timer}}</strong></span>
        </div>
    </div>

</template>

<script lang="ts">
    import { defineComponent, ref } from 'vue';
    import DataService from '@/services/DataService'
    import Data from '@/types/Data'
    import ResponseData from '@/types/ResponseData'

    export default defineComponent({
        name: 'WebContent',
        setup() {
            const Data = ref<Data[]>([])
            const TimerId = ref<number | undefined>(0)
            const Timer = ref<string | null>(// < genericz泛型 >, ( default value )
                new Date().toLocaleString("en-US", {
                    year: 'numeric', month: 'long', day: 'numeric',
                    hour: '2-digit', minute: '2-digit', second: '2-digit',
                    timeZoneName: 'long'
                })
            )
            return { Timer, TimerId, Data }// 初始值
        },
        methods: {// function區塊
            InitDiv(...DivId: string[]) {// 刷空訊息欄位
                DivId.forEach((item) => {
                    document.getElementById(item)!.innerHTML = ""
               })
            },
            StartLoading() {// 啟動等待效果
                let body = document.getElementById('Body')
                document.getElementById('spinnerGrop')!.style.display = "inline-flex"
                body!.style.opacity = "0.5"
                body!.style.overflow = "hidden"
                body!.style.cursor = "wait"
            },
            StopLoading() {// 停止等待效果
                let body = document.getElementById('Body')
                document.getElementById('spinnerGrop')!.style.display = "none"
                body!.style.opacity = "1"
                body!.style.overflow = "auto"
                body!.style.cursor = "default"
            },
            delay(milliseconds: number) {// 延遲效果
                return new Promise(resolve => {
                    setTimeout(resolve, milliseconds);
                });
            },
            closeAlert() {
                let Body = document.getElementById('Body')
                let body = document.getElementById('all')
                body!.style.opacity = "1"
                Body!.style.overflow = "auto"
                body!.style.cursor = "default"
                document.getElementById("LogOutWarn")!.style.display = "none"
            },
            showCheckAlert() {
                let Body = document.getElementById('Body')
                let body = document.getElementById('all')
                body!.style.opacity = "0.5"
                Body!.style.overflow = "hidden"
                body!.style.cursor = "wait"
                document.getElementById("LogOutWarn")!.style.display = "block"
            },
            showAlert() {
                let Body = document.getElementById('Body')
                let body = document.getElementById('all')
                body!.style.opacity = "0.5"
                Body!.style.overflow = "hidden"
                body!.style.cursor = "wait"
                document.getElementById('ErrorAlert')!.style.display = "block"
                setTimeout((time: number) => {
                    body!.style.opacity = "1"
                    Body!.style.overflow = "auto"
                    body!.style.cursor = "default"
                    this.$router.push("/login")
                }, 5000)
            },
            async LogOut() {
                this.closeAlert()
                this.StartLoading()
                await this.delay(1000)
                this.$route.params!.id = ""
                localStorage.removeItem('token')
                this.StopLoading()
                this.$router.push("/login")
            },
            async AuthCheck() {// 檢查憑證, 使用者權限
                this.StartLoading()
                await this.delay(1000);
                DataService.AuthCheck({Perm: 'perm'})
                    .then((response: ResponseData) => {
                        Object.values(response.data).forEach((item: any) => {
                            let Tag = document.getElementById((Object.values(item)[0]) as string + "Tag") as HTMLDivElement
                            let Bar = document.getElementById((Object.values(item)[0]) as string + "Bar") as HTMLDivElement
                            let UserAccount = this.$route.params!.id
                            if (Object.values(item)[1]) {
                                console.log(UserAccount)
                                Tag!.style.display = "inline-block"
                                Bar!.style.display = "block"
                                document.getElementById("UserAccount")!.innerHTML = " : " + ((UserAccount == "") ? "Anonmyous" : UserAccount.toString())
                            } else {
                                Tag!.style.display = "none"
                            }
                        })
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        this.StopLoading()
                        document.getElementById("ErrorAlertMsg")!.innerHTML = e.message
                        this.showAlert()
                    })

              this.StopLoading()
            },
            async GetAll() {// 取得所有資料
                this.StartLoading()
                await this.delay(1000);
                document.getElementById('GetAll_Response')!.style.display = "none"
                DataService.GetAll()
                    .then((response: ResponseData) => {
                        this.Data = response.data
                        document.getElementById('GetAll_Response')!.style.display = "block"
                        this.Data.forEach((item) => {
                            document.getElementById('GetAll_Response')!.innerHTML += JSON.stringify(item, null, 2)
                        })
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        document.getElementById('GetAll_ErrorMsg')!.innerHTML = "Error: " + e.message
                        this.StopLoading()
                    })
            },
            async Post() {// 上傳新資料
                this.StartLoading()
                this.delay(1000);
                document.getElementById('Post_Response')!.style.display = "none"
                let val = document.getElementById('PostData') as HTMLInputElement | null
                if (val == null || val!.value == "") {
                    document.getElementById('Post_ErrorMsg')!.innerHTML = "Error: input can't be null."
                    this.StopLoading()
                    return
                }
                DataService.Post({ data: val!.value, dateTime: val!.value })
                    .then((response: ResponseData) => {
                        this.Data = response.data
                        document.getElementById('Post_Response')!.style.display = "block"
                        this.Data.forEach((item) => {
                            document.getElementById('Post_Response')!.innerHTML += JSON.stringify(item, null, 2)
                        })
                        val!.value = ""
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        document.getElementById('Post_ErrorMsg')!.innerHTML = "Error: " + e.message
                        this.StopLoading()
                    })
            },
            async Get() {// 取得資料
                this.StartLoading()
                this.delay(1000);
                document.getElementById('Get_Response')!.style.display = "none"
                let val = document.getElementById('GetId') as HTMLInputElement | null
                if (val == null || val!.value == "") {
                    document.getElementById('Get_ErrorMsg')!.innerHTML = "Error: input can't be null."
                    this.StopLoading()
                    return
                }
                DataService.Get(val!.value)
                    .then((response: ResponseData) => {
                        this.Data = response.data
                        document.getElementById('Get_Response')!.style.display = "block"
                        document.getElementById('Get_Response')!.innerHTML += JSON.stringify(this.Data, null, 2)
                        val!.value = ""
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        document.getElementById('Get_ErrorMsg')!.innerHTML = "Error: " + e.message
                        this.StopLoading()
                    })
            },
            async Put() {// 更新資料
                this.StartLoading()
                this.delay(1000);
                document.getElementById('Put_Response')!.style.display = "none"
                let valId = document.getElementById('PutId') as HTMLInputElement | null
                let valData = document.getElementById('PutData') as HTMLInputElement | null
                if (valId == null || valId!.value == "" || valData == null || valData!.value == "") {
                    document.getElementById('Put_ErrorMsg')!.innerHTML = "Error: input can't be null."
                    this.StopLoading()
                    return
                }
                DataService.Update(valId!.value, { data: valData!.value, dateTime: valData!.value })
                    .then((response: ResponseData) => {
                        this.Data = response.data
                        document.getElementById('Put_Response')!.style.display = "block"
                        this.Data.forEach((item) => {
                            document.getElementById('Put_Response')!.innerHTML += JSON.stringify(item, null, 2)
                        })
                        valId!.value = ""
                        valData!.value = ""
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        document.getElementById('Put_ErrorMsg')!.innerHTML = "Error: " + e.message
                        this.StopLoading()
                    })
            },
            async Delete() {// 刪除資料
                this.StartLoading()
                this.delay(1000);
                document.getElementById('Delete_Response')!.style.display = "none"
                let val = document.getElementById('DeleteId') as HTMLInputElement | null
                if (val == null || val!.value == "") {
                    document.getElementById('Delete_ErrorMsg')!.innerHTML = "Error: input can't be null."
                    this.StopLoading()
                    return
                }
                DataService.Delete(val!.value)
                    .then((response: ResponseData) => {
                        this.Data = response.data
                        document.getElementById('Delete_Response')!.style.display = "block"
                        this.Data.forEach((item) => {
                            document.getElementById('Delete_Response')!.innerHTML += JSON.stringify(item, null, 2)
                        })
                        val!.value = ""
                        this.StopLoading()
                    })
                    .catch((e: Error) => {
                        document.getElementById('Delete_ErrorMsg')!.innerHTML = "Error: " + e.message
                        this.StopLoading()
                    })
            },
            DisplayTimer() {// 列出時間
                this.Timer = new Date().toLocaleString("en-US", {
                    year: 'numeric', month: 'long', day: 'numeric',
                    hour: '2-digit', minute: '2-digit', second: '2-digit',
                    timeZoneName: 'long'
                })
                return this.Timer
            },
            StartTimer() {// 開始計時
                this.TimerId = setInterval(() => this.DisplayTimer(), 1000);
            },
            StopTimer() {// 停止interval計時
                clearInterval(this.TimerId);
            }
        },
        created() {
            this.StartTimer()
        },
        mounted() {
            this.AuthCheck()
        }
    });
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .btn-logout {
        width: 20%;
        font-size: 1vw;
    }

    .accordion {
        opacity: 0.9;
    }
        .accordion:hover {
            opacity: 1;
        }

    .LogOut {
        margin: 2% 3% 0% 0%;
        top: 0;
        right: 0;
        position: fixed;
        font-size: 2.4vw;
        padding: 1.7vh 1vw 0.5vh 1vw;
        border: 0.24vw outset #ece6d9;
        border-radius: 55%;
        background-color: rgba(224, 215, 194, 0.4);
        transition: all 0.3s ease-in-out;
    }
        .LogOut:hover {
            background-color: rgba(248, 246, 241, 0.4);
            border: 0.24vw outset #ece6d9;
            border-radius: 50em;
        }

        .LogOut:active {
            border: 0.01vw outset #ece6d9;
            background-color: rgba(248, 246, 241, 0.2);
        }

    h2 {
        margin: 40px 0 20px 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
        font-size: 1vw;
    }
</style>
