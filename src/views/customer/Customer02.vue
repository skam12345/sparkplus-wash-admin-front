<template>
    <div>
        <div id="wrapper">
            <HeaderVue></HeaderVue>
            <nav>
                <ul class="main_menu">
                    <!-- 선택한 메뉴 li.is-current // 뎁스 공통 -->
                    <!-- 서브메뉴 있으면 li.is-sub 추가해주세요 -->
                    <li class="home">
                        <router-link to = "/Home">HOME</router-link>
                    </li>
                    <li class="sales is-sub">
                        <a>매출관리</a>
                        <ul class="sub_menu">
                            <li><router-link to = "/Sale01">매출관리</router-link></li>
                            <li><router-link to = "/Sale02">이용현황</router-link></li>
                        </ul>
                    </li>
                    <li class="customer is-sub is-current" >
                        <a>고객관리</a>
                        <ul class="sub_menu">
                            <li><router-link to = "/Customer01">회원조회</router-link></li>
                            <li class="is-current"><router-link to = "/Customer02">Fleet차량관리</router-link></li>
                            <li><router-link to = "/Customer03">멤버쉽조회</router-link></li>
                            <li><router-link to = "/Customer04">멤버쉽구독결제</router-link></li>
                            <li><router-link to = "/Customer05">멤버쉽알림톡발송</router-link></li>
                            <li><router-link to = "/Customer06">공지사항</router-link></li>
                        </ul>
                    </li>
                    <li class="promotion is-sub">
                        <a href="javascript:void(0);">프로모션</a>
                        <ul class="sub_menu">
                            <li><router-link to = "/Promotion01">프로모션관리</router-link></li>
                            <li><router-link to = "/Promotion02">쿠폰관리</router-link></li>
                            <li><router-link to = "/Promotion03">쿠폰발행</router-link></li>
                            <li><router-link to = "/Promotion04">Gift Card 교환</router-link></li>
                        </ul>
                    </li>
                    <li class="product is-sub">
                        <a href="javascript:void(0);">상품관리</a>
                        <ul class="sub_menu">
                            <li><router-link to = "/Product01">상품조회</router-link></li>
                            <!-- <li><router-link to = "/Product02">진열관리(상품)</router-link></li>
                            <li><router-link to = "/Product03">진열관리(옵션)</router-link></li> -->
                        </ul>
                    </li>
                    <li class="equipment is-sub">
                        <a href="javascript:void(0);">장비제어</a>
                        <ul class="sub_menu">
                            <!-- <li><router-link to = "/Equ01">장비제어</router-link></li> -->
                            <li><router-link to = "/Equ02">세차순서</router-link></li>
                            <!-- <li><router-link to = "/Equ03">이용현황</router-link></li> -->
                        </ul>
                    </li>
                    <li class="basics is-sub">
                        <a href="javascript:void(0);">기초관리</a>
                        <ul class="sub_menu">
                            <!-- <li><router-link to = "/Setting01">계정생성</router-link></li> -->
                            <li><router-link to = "/Setting02">근무자관리</router-link></li>
                            <!-- <li><router-link to = "/Setting03">장비/단말기 관리</router-link></li>
                            <li><router-link to = "/Setting04">기초코드관리</router-link></li> -->
                        </ul>
                    </li>
                </ul>
                <div class="info">
                    <p>(주)엔티아이</p>
                    사업자등록번호 : 504-81-15358 ㅣ 대표이사 : 김도연<br>대구광역시 서구 와룡로 335 1층 스파크플러스
                </div>
            </nav>
            <div id="container">
                <section class="sales">
                    <div class="breadcrumb">
                        <router-link to = "/Home">HOME</router-link>
                        <p>고객관리</p>
                        <p>Fleet차량관리</p>
                    </div>
                    <div class="contents">
                        <h2 class="title title_user">Fleet차량관리</h2>
                        <div class="contents_area">
                            <form autocomplete="off">
                                <div class="contents_area-search">
                                    <div class="select MT20">
                                        <div class="select_box MR30">
                                            <label for="">Fleetlist</label>
                                            <select v-model="selected_fleet" @change="getfleetcarlist($event)">
                                                <option disabled value="">Fleetlist</option>
                                                <option v-for="(info, index) in get_fleet" :value="info.fleet_no" :selected="index == 1" :key="index">
                                                    {{info.fleet_name}}
                                                </option>
                                            </select>
                                        </div>
                                    </div> 
                                </div>
                                
                                
                            </form>
                            <div class="contents_area-table">
                                <p class="contents_area-title">검색결과 <font class="fs14"></font></p>
                                <p class="btnRight">
                                <button type="button" class="btn_red" @click="deletecarlist" style="padding : 0px;">선택삭제</button>
                                <button type="button" class="btn_blue ML10" onclick="layerOpen('.layer_fleetcar_register')" style="padding : 0px;">차량등록</button>
                                <input id="fileUpload" @change="importExcel" type="file" hidden><button class="btn_blue ML10" @click="usefileupload" style="padding : 0px;">엑셀등록</button>
                            
                                </p>
                                <table>
                                    <colgroup>
                                        <col width="8%"/>
                                        <col width="10%"/>
                                        <col width=""/>
                                        <col width="30%"/>
                                    </colgroup>
                                    <thead>
                                        <tr>
                                            <th class="thht">선택</th>
                                            <th>No</th>
                                            <th>차량번호</th>
                                            <th>등록일자</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr v-for="(info, index) in get_fleetcarlist" v-show="setPaginate(index)" :key="index">
                                            <td class = "center">
                                                <input type="checkbox" :value="info.seq_no" v-model = "checkedCarList">
                                            </td>
                                            <td class="left">{{ get_fleetcarlist.length - index }}</td>
                                            <td class="left">{{ info.car_no }}</td>
                                            <td class="left">{{ info.reg_date }}</td>             
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
    
                        <div class="pagination">
                            <ul>
                                <li class="page first" :class="{'disable' : current == 1}">
                                    <a v-if="!(current==1)" href="javascript:void(0)" @click="updateCurrent(1)">first page</a>
                                    <a v-else>first page</a>
                                </li>
                                <li class="page prev" :class="{'disable' : current == 1}">
                                    <a v-if="!(current==1)" href="javascript:void(0)" @click="updateCurrent(current-1)">prev page</a>
                                    <a v-else>prev page</a>
                                </li>
    
    
                                <div v-for="page_index in paginate_total_unit" :key="page_index">
                                    <li class="num" @click.prevent="updateCurrent(page_index)" 
                                    :class="{'num is-current': page_index == current}" :key="page_index"> 
                                        <a href="">{{ page_index }}</a> 
                                    </li>
                                </div>
                                
    
    
    
                                <li class="page next" :class="{'disable' : current == paginate_total}">
                                    <a v-if="!(current==paginate_total)" href="javascript:void(0)" @click="updateCurrent(current+1)">next page</a>
                                    <a v-else>next page</a>
                                </li>
                                <li class="page last" :class="{'disable' : current == paginate_total}">
                                    <a v-if="!(current==paginate_total)" href="javascript:void(0)" @click="updateCurrent(paginate_total)">last page</a>
                                    <a v-else>last page</a>
                                </li>
                            </ul>
                        </div>
                    </div>
                </section>
            </div>
        </div>
        <div class="layer layer_fleetcar_register is-hidden">
            <form autocomplete="off" onSubmit="return false;">
                <div class="inner">
                    <div class="top">
                        <p class="popup_title">차량등록</p>
                    </div>
                    <div class="contents input MT20">
                        <div class="input_box MB40">
                            <label for="title">차량번호</label>
                            <input type="text" id="title" v-model ="car_no" placeholder="차량 번호">
                        </div>
                    </div>
                    <div class="btn_group2">
                        <button type="button" class="btn_white" onclick="layerClose('.layer_fleetcar_register')">취소</button>
                        <button type="button" class="btn_blue" @click="set_insertfleetcar">등록</button>
                    </div>
                    <button type="button" class="btn_close" onclick="layerClose('.layer_fleetcar_register')">닫기</button>
                </div>
            </form>
        </div>
    </div>
    </template>
    <script>
        import * as Xlsx from 'xlsx'
        export default{
            computed:{
                maxPage() {  // 총 페이지 수(and 최대 페이지 번호)
                    return this.paginate_total
                },
                startPage() { // 페이지 시작 번호
                    return (Math.trunc((this.current - 1) / this.pageCount) * this.pageCount) + 1
                },
                endPage() { // 페이지 끝 번호
                    let end = this.startPage + this.pageCount - 1
                    return end < this.maxPage ? end : this.maxPage
                },
                paginate_total_unit(){
                    let units = [];
                    for(let num = this.startPage;num <=this.endPage;num++){
                        units.push(num);
                    }
                    return units;
                },
                revise_pay(){
                    return this.return_one(this.revise.pay_fee);
                }
            },
            data(){
                return{
                    items :'',
                    excelJsonData : '',
                    get_fleet : [],
                    get_fleetcarlist : [],
                    selected_car : [],
                    sea_date_start: '',
                    sea_date_end: '',
                    car_no : '',
                    selected_fleet : '',
                    sea_carnum: '',
                    get_paysum: '',
                    get_payresult: '',
                    paginate : 25,
                    paginate_total: 0,
                    current: 1,
                    pageCount : 10, // 페이지 버튼 최대 개수
                    checkedCarList : [],
                }
            },
            created(){
                this.set_yes();
                this.get_fleetlist();
            },
            methods : {
                set_insertfleetcar(){
                    console.log(this.selected_fleet);
                    if(this.selected_fleet != ''){
                        this.$http.post(this.$server+'/admin/setFleetCarInsert',{
                        fleet_no : this.selected_fleet,
                        car_no : this.car_no
                        },
                        {headers : {
                            auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                            }
                        }).then((res) => {                   
                            console.log(res.data);
                                if(res.data.result_code == "Y"){
                                    this.$http.post(this.$server+'/admin/getFleetCarList',{
                                fleet_no : this.selected_fleet
                                },
                                {headers : {
                                    auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                                    }
                                }).then((res) => {                   
                                    this.get_fleetcarlist = res.data;
                                    // $('.layer_fleetcar_register').removeClass('is-open').addClass('is-hidden');
                                    // $('body').removeClass('layer-opens');
                                })
                            }
                        })
                    }else{
                        alert('플릿리스트를 확인해주세요');
                        // $('.layer_fleetcar_register').removeClass('is-open').addClass('is-hidden');
                        // $('body').removeClass('layer-opens');
                    }
                },
                usefileupload() {
                    if(this.selected_fleet != ''){
                        document.getElementById("fileUpload").click()
                    }else{
                        alert('플릿리스트를 확인해주세요');
                    }
                },
                importExcel() {
                    let input = event.target;
                    let reader = new FileReader();
                        
                        reader.onload = () => {
                        let data = reader.result;
                        let workBook = Xlsx.read(data, { type: 'binary' });
                        workBook.SheetNames.forEach(sheetName => {
                            let rows = Xlsx.utils.sheet_to_json(workBook.Sheets[sheetName]);
                            this.items = rows;
                        });
                            console.log(this.items); 
                            for(var i =0; i<this.items.length; i++){
                            this.$http.post(this.$server+'/admin/setFleetCarInsert',{
                            fleet_no : this.selected_fleet,
                            car_no : this.items[i].car_no
                        },
                        {headers : {
                            auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                            }
                        }).then((res) => {                   
                        console.log(res.data);
                            if(res.data.result_code == "Y"){
                                this.$http.post(this.$server+'/admin/getFleetCarList',{
                                fleet_no : this.selected_fleet
                                },
                                {headers : {
                                    auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                                    }
                                }).then((res) => {                   
                                    this.get_fleetcarlist = res.data;
                                })
                            }
                        })
                        }               
                    };
                    reader.readAsBinaryString(input.files[0]);
                },
                deletecarlist(){
                    if(this.selected_fleet != ''){
                         if(this.checkedCarList.length > 0){
                        var result = confirm(this.checkedCarList.length+'건의 차량을 삭제하시겠습니까?')
                        if(result){
                            console.log(this.checkedCarList[1]);
                            for(var i =0; i<this.checkedCarList.length; i++){
                                this.$http.post(this.$server+'/admin/setFleetCarDelete',{
                                    seq_no : this.checkedCarList[i]
                                },
                                {headers : {
                                    auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                                    }
                                }).then((res) => {                   
                                    if(res.data.result_code == "Y"){
                                        this.$http.post(this.$server+'/admin/getFleetCarList',{
                                        fleet_no : this.selected_fleet
                                        },
                                        {headers : {
                                            auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                                            }
                                        }).then((res) => {                   
                                            this.get_fleetcarlist = res.data;
                                        })
                                    }
                                })
                            }  
                            this.checkedCarList = [];
                        }
                        }else{
                            alert("항목을 선택해주세요");
                        }
                    }else{
                        alert('플릿리스트를 확인해주세요');
                    }
                },
                get_fleetlist(){
                     this.$http.post(this.$server+'/admin/getFleetList',{
    
                     },
                    {headers : {
                        auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                        }
                    }).then((res) => {                   
                        this.get_fleet = res.data;
                    })
                },
                getfleetcarlist:function(event){
                    console.log(event.target.value);
                    this.$http.post(this.$server+'/admin/getFleetCarList',{
                        fleet_no : this.selected_fleet
                     },
                    {headers : {
                        auth_key :'c83b4631-ff58-43b9-8646-024b12193202'
                        }
                    }).then((res) => {                   
                        this.get_fleetcarlist = res.data;
                        console.log(this.get_fleetcarlist);
                    })
                },
                return_one(on_num){
                    if(on_num != undefined){
                        const parts = on_num.toString().split('.');
                        parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ',');
                        return parts.join('.');
                    }  
                },
                setPaginate: function (i) {
                    if (this.current == 1) {
                        return i < this.paginate;
                    }
                    else {
                        return (i >= (this.paginate * (this.current - 1)) && i < (this.current * this.paginate));
                    }
                },
                updateCurrent: function (i) {
                    this.current = i;
    
                },
                set_yes: function(){
                    const d = new Date();
                    const b = new Date();
                    const year = d.getFullYear(); // 년
                    const month = (d.getMonth()+1);   // 월
                    const day = d.getDate();
                    var pastDate = b.getDate() - 1;
                    b.setDate(pastDate);
                    const b_year = b.getFullYear(); // 년
                    const b_month = (b.getMonth()+1);   // 월
                    const b_day = b.getDate();
                    this.sea_date_start = b_year+'-'+b_month.toString().padStart(2,'0')+'-'+b_day.toString().padStart(2,'0')
                    this.sea_date_end = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                },
                set_today: function(){
                    const d = new Date();
                    const year = d.getFullYear(); // 년
                    const month = (d.getMonth()+1);   // 월
                    const day = d.getDate();
                    this.sea_date_start = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                    this.sea_date_end = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                },
                set_weak: function(){
                    const d = new Date();
                    const b = new Date();
                    const year = d.getFullYear(); // 년
                    const month = (d.getMonth()+1);   // 월
                    const day = d.getDate();
                    var pastDate = b.getDate() - 7;
                    b.setDate(pastDate);
                    const b_year = b.getFullYear(); // 년
                    const b_month = (b.getMonth()+1);   // 월
                    const b_day = b.getDate();
                    this.sea_date_start = b_year+'-'+b_month.toString().padStart(2,'0')+'-'+b_day.toString().padStart(2,'0')
                    this.sea_date_end = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                },
                set_month: function(){
                    const d = new Date();
                    const b = new Date();
                    const year = d.getFullYear(); // 년
                    const month = (d.getMonth()+1);   // 월
                    const day = d.getDate();
                    var pastDate = b.getMonth() - 1;
                    b.setDate(pastDate);
                    const b_year = b.getFullYear(); // 년
                    const b_month = (b.getMonth());   // 월
                    const b_day = b.getDate();
                    this.sea_date_start = b_year+'-'+b_month.toString().padStart(2,'0')+'-'+b_day.toString().padStart(2,'0')
                    this.sea_date_end = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                },
                set_year: function(){
                    const d = new Date();
                    const year = d.getFullYear(); // 년
                    const month = (d.getMonth()+1);   // 월
                    const day = d.getDate();
                    this.sea_date_start = year+'-'+month.toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                    this.sea_date_end = year+'-'+(month-1).toString().padStart(2,'0')+'-'+day.toString().padStart(2,'0')
                },
                return_date(date){
                    var today = new Date(date);
                    today.setHours(today.getHours() + 9);
                    return today.toISOString().replace('T', ' ').substring(0, 19);
                },
                makeExcelFile5 () {
                    const workBook = Xlsx.utils.book_new()
                    const workSheet = Xlsx.utils.json_to_sheet(this.get_payresult)
                    Xlsx.utils.book_append_sheet(workBook, workSheet, '매출')
                    Xlsx.writeFile(workBook, 'output.xlsx')
                },
            }
        }
    
    </script>