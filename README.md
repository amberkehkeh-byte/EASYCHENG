# EASYCHENG
點名冊
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>安親班點名系統</title>
  <style>
    body { font-family: "Microsoft JhengHei", sans-serif; margin: 20px; }
    h1 { text-align: center; }
    .class-section { margin-bottom: 40px; }
    .students { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 10px; }
    .student {
      padding: 8px 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
      cursor: pointer;
      user-select: none;
    }
    .present { background-color: #c8f7c5; }   /* 到課 */
    .sick { background-color: #f8c5c5; color: red; } /* 病假 */
    .absent { background-color: #c5d8f8; color: blue; } /* 固定不到 */
    .stats { font-size: 14px; margin-top: 5px; }
  </style>
</head>
<body>
  <h1>安親班點名系統</h1>

  <div id="classes"></div>

  <script>
    const classLists = {
      "A班": [
        "邱館玟","周永哲","李明希","莊瑋澤","廖威盛","戴云安","邱汝禎","沈可若",
        "郭芊諺","周毓瑄","邱立晴","黃茜涵","陳苡臻","簡心恩","凌翊嘉","張昀庭","曾禹寧"
      ],
      "B班": [
        "林俊曄","呂妍秦","陳明秦","邱延恩","張柏中","吳孝柔","羅嘉賢","彭紫頤","劉宇峰",
        "沈鎧閔","曹雨恩","白若妍","楊岳庭","盧亮宇","林妍均","蘇欽駿","陳汝諺","廖俞融","黃若霙"
      ],
      "C班": [
        "徐千喬","周浚飛","徐重恩","劉宇宸","陳郁婷","詹詠瀅","楊氏玉瑄","盧嘉安","張依婷","張奕竹",
        "羅翔靖","涂恩頤","吳宇勛","趙芸澔","呂芷芸","莊琮禾","林于瑄","黃思妤","莊珮妤","黃芷妤"
      ],
      "D班": [
        "鍾翔丞","鍾浚羽","鄭元凱","方歆明","楊勝智","邱馬希","趙育霖","黃梓玉","吳希柔",
        "陳姿伶","彭芷筠","楊凱庭","邱丞駿","王聲逸","涂恩捷","周瀛杰","豐張念蓁","莊芸妤"
      ]
    };

    const container = document.getElementById("classes");

    function updateStats(section) {
      const students = section.querySelectorAll(".student");
      let present = 0, sick = 0, absent = 0;
      students.forEach(div => {
        if (div.classList.contains("present")) present++;
        else if (div.classList.contains("sick")) sick++;
        else if (div.classList.contains("absent")) absent++;
      });
      const total = students.length;
      section.querySelector(".stats").innerText =
        `✅ 到課: ${present}　🤒 病假: ${sick}　🚫 固定不到: ${absent}　👥 總人數: ${total}`;
    }

    Object.entries(classLists).forEach(([className, students]) => {
      const section = document.createElement("div");
      section.className = "class-section";
      section.innerHTML = `<h2>${className}</h2>`;

      const studentDiv = document.createElement("div");
      studentDiv.className = "students";

      students.forEach(name => {
        const div = document.createElement("div");
        div.className = "student";
        div.innerText = name;

        // 點擊切換狀態
        div.addEventListener("click", () => {
          if (div.classList.contains("present")) {
            div.classList.remove("present");
            div.classList.add("sick");
          } else if (div.classList.contains("sick")) {
            div.classList.remove("sick");
            div.classList.add("absent");
          } else if (div.classList.contains("absent")) {
            div.classList.remove("absent");
          } else {
            div.classList.add("present");
          }
          updateStats(section);
        });

        studentDiv.appendChild(div);
      });

      section.appendChild(studentDiv);

      const statsDiv = document.createElement("div");
      statsDiv.className = "stats";
      section.appendChild(statsDiv);

      container.appendChild(section);
      updateStats(section);
    });
  </script>
</body>
</html>
