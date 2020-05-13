<template>
    <div>
        <div class="title">
            DO Converter(Darken, Lighten)
        </div>
        <div id="formBox">
            <form class="clearfix">
                <div class="color">
                    #<input class="form-control input-lg" type="text" name="colorCode" value="" placeholder="000000"/>
                </div>
                <div class="percent">
                    <span>/</span>
                    <input class="form-control input-lg" type="text" name="percent" value="" placeholder="5"/>
                    %
                </div>
            </form>
        </div>
        <div id="content">
            <div id="lighten" class="colorBox clearfix" style="display: block;"></div>
            <br>
            <div id="darken" class="colorBox clearfix" style="display: block;"></div>
        </div>
    </div>
</template>
<script>
    import $ from 'jquery';
    import tinycolor from "tinycolor2";
    export default {
        name: "Converter",
        mounted() {
          var _this = this;
            $('.percent input').keyup(function() {
                _this.converter();
            });
        },
        methods : {
            converter : function() {
                var color = $(".color input").val();

                if($('.color input').val().length == 6 && !$('.percent input').val() == ""){
                    $(".colorBox").html("");
                    var percent = $(".percent input").val();
                    percent = parseInt(percent);

                    var t = tinycolor(color);
                    var hsl = t.toHsl();  // { h: 0, s:1, l: 0.5 }

                    var colorH = hsl["h"];
                    var colorS = hsl["s"] * 100;
                    var colorL = hsl["l"] * 100;

                    $("#lighten").append("<h2>lighten</h2>");
                    $("#darken").append("<h2>darken</h2>");

                    for (var i = 0; i < 100; i = i + percent){

                        var lighten = colorL + i;
                        var lightColor = tinycolor("hsl(" + colorH + ", " + colorS + "%, " + lighten + "%)");
                        var lightHex = lightColor.toHexString();

                        var darken = colorL - i;
                        var darkColor = tinycolor("hsl(" + colorH + ", " + colorS + "%, " + darken + "%)");
                        var darkHex = darkColor.toHexString();

                        if(lighten <= 100){
                            $("#lighten").append("<div class='c" + i + "'><span style='background: " + lightHex + "'></span><p>" + i + "%<br>" + lightHex + "</p></div>").hide().delay(0).fadeIn("fast");
                        }

                        if(darken >= 0){
                            $("#darken").append("<div class='c" + i + "'><span style='background: " + darkHex + "'></span><p>" + i + "%<br>" + darkHex + "</p></div>").hide().delay(50).fadeIn("fast");
                        }
                    }
                    return false;
                }
            }
        }
    };
</script>
<style>
    .title {
        text-align:center;
        font-size:20px;
        font-weight:bold;
        padding-top:20px;
        color:#999;
    }
    #formBox {
        background: #00a1b9;
        margin: 30px 0 5px;
        padding: 30px 0 28px;
        font-size: 140%;
    }
    #formBox form {
        text-align: center;
    }
    #formBox form .color .form-control {
        border: 4px solid #0392a7;
        width: 260px;
        display: inline;
        height: 55px;
    }
    #formBox form .percent .form-control {
        border: 4px solid #0392a7;
        width: 70px;
        height: 55px;
        display: inline;
        text-align: right;
    }
    #formBox form .color {
        display: inline-block;
    }
    #formBox form .percent {
        display: inline-block;
        margin-left: 5px;
    }
    .colorBox div p {
        font-size: 80%;
    }

    p {
        margin: 0 0 10px;
    }
    .clearfix:before, .clearfix:after {
        display: table;
        content: " ";
    }
    .colorBox div {
        float: left;
        width: 50px;
        margin: 0 15px 10px 0;
        color: #777;
    }
    .colorBox div span {
        display: block;
        width: 50px;
        height: 50px;
        margin: 3px 0 4px;
    }
    body {
        font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
        font-size: 14px;
        line-height: 1.428571429;
        color: #333;
        background-color: #fff;
    }
    .colorBox h2 {
        margin-bottom: 15px;
        font-size: 180%;
    }

    h2 {
        font-family: 'Open Sans', sans-serif;
    }

    #content {
        width: 850px;
        margin: 0 auto 30px;
    }
</style>