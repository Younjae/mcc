<template>
    <form class ="registerform" style="width: 100%; height: 100%;" action="/admin/register" method="POST" enctype="multipart/form-data">
        <fieldset class="registerset">
            <table style="table-layout: fixed; height: 600px; margin:30px">
                <tr>
                    <td class ="head" colspan="2">
                        <h1>MMC 카드 등록</h1>
                    </td>
                </tr>
                <tr>
                    <td style="padding-right:100px;">
                        <input type="text" id="cardName" name="cardName" placeholder="카드 이름"/>
                        <br>
                        <br>
                        <br>
                        <h3 style="margin-top:20px; margin-bottom:20px;">은행사 선택</h3>
                        <div class="menubar" >
                            <select id="select1" name="selectCard">
                            </select>
                        </div>
                        <br>
                        <br>
                    
                        <h3>이미지 업로드</h3>
                        
                        <gb-inputfile v-bind:prolabel="label" v-bind:proaccept="accept" v-bind:prohint="hint" v-bind:prowidth="width"></gb-inputfile>

                    </td>
                    <td>
                        <h3>혜택 분류 선택</h3>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkCaffe" name="1" value="checkCaffe" /><label for="checkCaffe"> <span></span>카페/디저트</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkTrip" name="2" value="checkTrip" /><label for="checkTrip"> <span></span>여행/숙박</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkMovie" name="3" value="checkMovie" /><label for="checkMovie"> <span></span>영화/문화</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkTraffic" name="4" value="checkTraffic" /><label for="checkTraffic"> <span></span>교통</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkTel" name="5" value="checkTel" /><label for="checkTel"> <span></span>통신</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkAir" name="6" value="checkAir" /><label for="checkAir"> <span></span>항공</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkFood" name="7" value="checkFood" /><label for="checkFood"> <span></span>음식</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkShopping" name="8" value="checkShopping" /><label for="checkShopping"> <span></span>쇼핑</label>
                        </div>
                        <div style="margin-bottom:10px">
                        <input type="checkbox" id="checkHospital" name="9" value="checkHospital" /><label for="checkHospital"> <span></span>병원</label>
                        </div>
                    </td>
                </tr>
                <tr><td colspan="2" class="head"><input type="text" id="cardDetail" name="cardDetail" placeholder="카드 상세 정보" style="width:400px; margin:30px;"/></td></tr>
                <tr><td colspan="2" class="head"><input type="submit" value="등록"></td></tr>
            </table>
        </fieldset>
    </form>
</template>

<script>
    import InputFile from '../components/gb-fileupload.vue'
    import axios from 'axios'
    export default{
    beforeCreate: function(){
        axios.get('/admin/register/getbank') .then(res => { // 불러온 값을 Console에 뿌려줍니다. 
            var data = res.data;
            for(var key in data) {
                var op = new Option();
                op.value = key; // 값 설정
                op.text = data[key]; // 텍스트 설정
                document.getElementById( "select1" ).options.add(op);
            }
        });
    },
        components:{
        'gb-inputfile': InputFile
        },
  
        data(){
            return{
                hint: '이미지 파일만 가능합니다',
                label: 'File',
                accept: '.gif, .jpg, .png',
                width: 'width: 100px'
            }
        }
    }
</script>

<style scoped>
    body, html{
        height: 100%;
    }
    .registerform{
        position: relative;
        display: flex;
        justify-content: center;
        vertical-align: middle;
        margin-top: auto;
         margin-bottom: 200px;/*auto; */
    }
    .registerset{
        height:auto;
        margin-top: auto;
        margin-bottom: auto;
        background:aliceblue;
        padding: 10px;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        -webkit-box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        -moz-box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        border-radius: 5px;
    }

    td{
        text-align: left;
    }
    input[type="checkbox"] {
    display:none;
    }
    input[type="checkbox"] + label span {
    display: inline-block;
    width: 24px;
    height: 24px;
    margin: -2px 10px 0 0;
    vertical-align: middle;
    background: url(../img/checkbox.svg) left top no-repeat;
    cursor: pointer;
    background-size: cover;
    }
    input[type="checkbox"]:checked + label span {
    background:url(../img/checkbox.svg)  -26px top no-repeat;
    background-size: cover;
    }

    select {
    width: 200px;
    padding: .8em .5em;
    border: 1px solid #999;
    font-family: inherit;
    
    background: url(../img/arrow.png) no-repeat 95% 50%;
    background-color: #fff;
    border-radius: 0px;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    }
    .head{
        text-align: center;
    }
    input[type="text"], 
    input[type="password"]{
        width: 180px; 
        height: auto; /* 높이 초기화 */ 
        line-height: normal; /* line-height 초기화 */ 
        padding: .8em .5em; /* 여백 설정 */
    }
    input[type="submit"] {
    background:midnightblue;
    border: 3px solid #fff;
    border-radius: 5px;
    color: #fff;
    display: block;
    font-size: 1em;
    font-weight: bold;
    margin: 1em auto;
    padding: .5em 1.5em;
    position: relative;
    text-transform: uppercase;
    }

</style>