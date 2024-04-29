---
title: 用JQuery和CSS3制作漂亮的数字时钟
link: jquery-css3-clock
tags:
  - CSS3
  - html5
  - jquery
  - 代码
  - 分享
id: '498'
categories:
  - - 分享
date: 2013-06-20 11:17:03
---

有些时候，不得不感叹**CSS3**和**JQuery**结合的妙用，这一刻，感觉世界是多么美好，多么和谐。 分享一个非常漂亮的用CSS3和Jquery制作的数字时钟，还能切换主题，分别是黑色的和白色的，呃，个人比较喜欢黑色的那款。接下来是分享作者的制作过程。 ![clock](http://vsnote.test/wp-content/uploads/2013/06/clock.jpg)  

#### html代码

主容器是ID为clock的元素，而里面的星期几，上午还是下午，时间，闹钟都在.display元素里面。下面是生成数字时要用到的html。

.digits元素里面用了6个这样用7个span组成的div，他们的任务就是组成一个有效的时间。下面是一个示意图。 ![the_digits_explained](http://vsnote.test/wp-content/uploads/2013/06/the_digits_explained.jpg)

#### 数字说明

它们完全用CSS样式渲染且默认设置为 opacity:0 。定义在它们父div上的样式将决定它们的可见性。下面是数字“0”的CSS： assets/css/styles.css

/\* 0 \*/
 
#clock .digits div.zero .d1,
#clock .digits div.zero .d3,
#clock .digits div.zero .d4,
#clock .digits div.zero .d5,
#clock .digits div.zero .d6,
#clock .digits div.zero .d7{
    opacity:1;
}

除了中间一个，所有的片段都是可见的，这些span上添加了CSS3转换属性，当在数字之间切换时出现渐变效果。 样式表里有很多其他CSS，就不在这里一一列举了。相信学习CSS的最好方法就是观察它在Firebug、Chrome或者其他浏览器里面的demo代码。 ![the_white_theme](http://vsnote.test/wp-content/uploads/2013/06/the_white_theme.jpg) 很明显，上面展示的是一个白色主题的数字时钟。  要想要时钟工作，我们将使用jQuery生成每个数字的标签，并且设置一个定时器每秒钟更新一次样式，为了更简单，我们使用moment.js(一个处理时间和日期的js库) 库来填补JavaScript原生日期和时间方法的缺陷。 assets/js/script.js

$(function(){
 
    // Cache some selectors
 
    var clock = $('#clock'),
        alarm = clock.find('.alarm'),
        ampm = clock.find('.ampm');
 
    // Map digits to their names (this will be an array)
    var digit\_to\_name = 'zero one two three four five six seven eight nine'.split(' ');
 
    // This object will hold the digit elements
    var digits = {};
 
    // Positions for the hours, minutes, and seconds
    var positions = \[
        'h1', 'h2', ':', 'm1', 'm2', ':', 's1', 's2'
    \];
 
    // Generate the digits with the needed markup,
    // and add them to the clock
 
    var digit\_holder = clock.find('.digits');
 
    $.each(positions, function(){
 
        if(this == ':'){
            digit\_holder.append('

');
        }
        else{
 
            var pos = $('

');
 
            for(var i=1; i<8; i++){
                pos.append('');
            }
 
            // Set the digits as key:value pairs in the digits object
            digits\[this\] = pos;
 
            // Add the digit elements to the page
            digit\_holder.append(pos);
        }
 
    });
 
    // Add the weekday names
 
    var weekday\_names = 'MON TUE WED THU FRI SAT SUN'.split(' '),
        weekday\_holder = clock.find('.weekdays');
 
    $.each(weekday\_names, function(){
        weekday\_holder.append('' + this + '');
    });
 
    var weekdays = clock.find('.weekdays span');
 
    // Run a timer every second and update the clock
 
    (function update\_time(){
 
        // Use moment.js to output the current time as a string
        // hh is for the hours in 12-hour format,
        // mm - minutes, ss-seconds (all with leading zeroes),
        // d is for day of week and A is for AM/PM
 
        var now = moment().format("hhmmssdA");
 
        digits.h1.attr('class', digit\_to\_name\[now\[0\]\]);
        digits.h2.attr('class', digit\_to\_name\[now\[1\]\]);
        digits.m1.attr('class', digit\_to\_name\[now\[2\]\]);
        digits.m2.attr('class', digit\_to\_name\[now\[3\]\]);
        digits.s1.attr('class', digit\_to\_name\[now\[4\]\]);
        digits.s2.attr('class', digit\_to\_name\[now\[5\]\]);
 
        // The library returns Sunday as the first day of the week.
        // Stupid, I know. Lets shift all the days one position down,
        // and make Sunday last
 
        var dow = now\[6\];
        dow--;
 
        // Sunday!
        if(dow < 0){
            // Make it last
            dow = 6;
        }
 
        // Mark the active day of the week
        weekdays.removeClass('active').eq(dow).addClass('active');
 
        // Set the am/pm text:
        ampm.text(now\[7\]+now\[8\]);
 
        // Schedule this function to be run again in 1 sec
        setTimeout(update\_time, 1000);
 
    })();
 
    // Switch the theme
 
    $('a.button').click(function(){
        clock.toggleClass('light dark');
    });
 
}); 

这里面最关键的就是 update\_time 方法，在它里面，我们获取到当前日期作为一个字符串，并且使用它来填充时钟元素并且给数字设置正确的样式。 [Demo](http://demo.tutorialzine.com/2013/06/digital-clock/ "查看 Demo") [下载](http://demo.tutorialzine.com/2013/06/digital-clock/digital-clock.zip "点此下载")

> 原文地址：[http://tutorialzine.com/2013/06/digital-clock/](http://tutorialzine.com/2013/06/digital-clock/ "查看原文")