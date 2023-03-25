var local = window.localStorage;
var body = document.getElementById("body");
let day_str = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
let month_str =
    ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
var day, hour, sec, minute, month, session, date, wish;

function common(bgcolor, color, clockclr, opposite_theme) {
    body.style.backgroundColor = bgcolor;
    body.style.color = color;
    box("#toggleButton", color);
    box("#clock", clockclr);
    local.setItem("themeTo", opposite_theme);
}
setInterval(() => {
    var time = new Date();
    date = time.getDate();
    hour = time.getHours();
    minute = time.getMinutes();
    sec = time.getSeconds();
    month = time.getMonth();
    day = time.getDay();
    
    (hour < 12) ? session = "AM" : session = "PM";
    hour = (hour < 10) ? "0" + hour : hour;
    minute = (minute < 10) ? "0" + minute : minute;
    sec = (sec < 10) ? "0" + sec : sec;
    document.getElementById("time").innerText = `${hour} : ${minute} : ${sec}  ${session}`;
    
    document.getElementById("second").style.transform = "rotate(" + (sec * 6) + "deg)";
    document.getElementById("minute").style.transform = "rotate(" + (minute * 6) + "deg)";
    document.getElementById("hour").style.transform = "rotate(" + (30 * hour + minute / 2) + "deg)";

    document.getElementById("date").innerText = `${day_str[day]} ${month_str[month]} ${date}`;
}, 1000);
window.addEventListener("load", () => {
    if (local.getItem("themeTo") == null) { local.setItem("themeTo", "Dark"); }
    (local.getItem("themeTo") == "Dark") ?
        common("white", "black", "black", "Dark") :
        common("black", "white", "aqua", "Light");
});
function darkTheme() {
    (local.getItem("themeTo") == "Dark") ?
        common("black", "white", "aqua", "Light") :
        common("white", "black", "black", "Dark");
}