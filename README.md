<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💫 星座配对</title>
<style>
*{margin:0;padding:0;}
body{background:linear-gradient(135deg,#0c0c1e,#1a0b2e);display:flex;justify-content:center;align-items:center;min-height:100vh;font-family:'Arial',sans-serif;}
#box{background:rgba(255,255,255,0.08);backdrop-filter:blur(20px);border-radius:40px;padding:35px;width:350px;border:1px solid rgba(255,255,255,0.1);box-shadow:0 20px 60px rgba(100,50,200,0.2);}
h2{color:#c8a8ff;text-align:center;font-size:28px;margin-bottom:20px;}
select{width:100%;padding:14px;margin:8px 0;border-radius:15px;border:none;background:rgba(255,255,255,0.1);color:#fff;font-size:18px;outline:none;appearance:none;cursor:pointer;}
select option{background:#1a0b2e;color:#fff;}
#matchBtn{width:100%;padding:16px;margin:15px 0;border:none;border-radius:20px;background:linear-gradient(135deg,#a78bfa,#7c3aed);color:#fff;font-size:20px;font-weight:bold;cursor:pointer;transition:transform 0.2s;box-shadow:0 8px 30px rgba(124,58,237,0.3);}
#matchBtn:active{transform:scale(0.95);}
#result{background:rgba(255,255,255,0.05);border-radius:20px;padding:25px;margin-top:15px;text-align:center;min-height:100px;display:none;}
#result .score{font-size:48px;font-weight:bold;color:#a78bfa;}
#result .text{color:#c8a8ff;font-size:18px;margin-top:10px;line-height:1.6;}
</style>
</head>
<body>
<div id="box">
    <h2>💫 星座配对</h2>
    <select id="sign1">
        <option value="0">♉ 金牛座</option><option value="1">♈ 白羊座</option>
        <option value="2">♊ 双子座</option><option value="3">♋ 巨蟹座</option>
        <option value="4">♌ 狮子座</option><option value="5">♍ 处女座</option>
        <option value="6">♎ 天秤座</option><option value="7">♏ 天蝎座</option>
        <option value="8">♐ 射手座</option><option value="9">♑ 摩羯座</option>
        <option value="10">♒ 水瓶座</option><option value="11">♓ 双鱼座</option>
    </select>
    <select id="sign2">
        <option value="0">♉ 金牛座</option><option value="1">♈ 白羊座</option>
        <option value="2">♊ 双子座</option><option value="3">♋ 巨蟹座</option>
        <option value="4">♌ 狮子座</option><option value="5">♍ 处女座</option>
        <option value="6">♎ 天秤座</option><option value="7">♏ 天蝎座</option>
        <option value="8">♐ 射手座</option><option value="9">♑ 摩羯座</option>
        <option value="10">♒ 水瓶座</option><option value="11">♓ 双鱼座</option>
    </select>
    <button id="matchBtn">💕 查看配对</button>
    <div id="result">
        <div class="score" id="scoreDisplay">95%</div>
        <div class="text" id="textDisplay">你们是天造地设的一对！</div>
    </div>
</div>
<script>
const matchData={
    '0':{name:'金牛',compat:{0:85,1:70,2:90,3:75,4:95,5:60,6:80,7:70,8:90,9:65,10:75,11:85}},
    '1':{name:'白羊',compat:{0:70,1:90,2:65,3:95,4:75,5:85,6:70,7:80,8:65,9:90,10:80,11:75}},
    '2':{name:'双子',compat:{0:90,1:65,2:80,3:70,4:85,5:75,6:95,7:70,8:90,9:65,10:85,11:80}},
    '3':{name:'巨蟹',compat:{0:75,1:95,2:70,3:85,4:70,5:80,6:75,7:90,8:65,9:85,10:70,11:95}},
    '4':{name:'狮子',compat:{0:95,1:75,2:85,3:70,4:80,5:65,6:90,7:85,8:95,9:70,10:80,11:75}},
    '5':{name:'处女',compat:{0:60,1:85,2:75,3:80,4:65,5:90,6:80,7:95,8:70,9:85,10:75,11:70}},
    '6':{name:'天秤',compat:{0:80,1:70,2:95,3:75,4:90,5:80,6:85,7:75,8:85,9:70,10:95,11:80}},
    '7':{name:'天蝎',compat:{0:70,1:80,2:70,3:90,4:85,5:95,6:75,7:80,8:75,9:85,10:70,11:90}},
    '8':{name:'射手',compat:{0:90,1:65,2:90,3:65,4:95,5:70,6:85,7:75,8:80,9:70,10:85,11:80}},
    '9':{name:'摩羯',compat:{0:65,1:90,2:65,3:85,4:70,5:85,6:70,7:85,8:70,9:90,10:75,11:80}},
    '10':{name:'水瓶',compat:{0:75,1:80,2:85,3:70,4:80,5:75,6:95,7:70,8:85,9:75,10:80,11:85}},
    '11':{name:'双鱼',compat:{0:85,1:75,2:80,3:95,4:75,5:70,6:80,7:90,8:80,9:80,10:85,11:90}}
};
const quotes=[
    '✨ ltx和wzx是天生一对',
    '💕 ltx和wzx是天生一对',
    '🌙 ltx和wzx是天生一对',
    '⭐ ltx和wzx是天生一对',
    '🌸 ltx和wzx是天生一对',
    '💫 ltx和wzx是天生一对'
];
document.getElementById('matchBtn').addEventListener('click',function(){
    const s1=parseInt(document.getElementById('sign1').value);
    const s2=parseInt(document.getElementById('sign2').value);
    const score=matchData[s1].compat[s2]+Math.floor(Math.random()*10-5);
    const finalScore=Math.min(100,Math.max(50,score));
    document.getElementById('scoreDisplay').textContent=finalScore+'%';
    document.getElementById('textDisplay').textContent=quotes[Math.floor(Math.random()*quotes.length)];
    document.getElementById('result').style.display='block';
    this.style.transform='scale(0.95)';
    setTimeout(()=>this.style.transform='scale(1)',200);
});
</script>
</body>
</html>
