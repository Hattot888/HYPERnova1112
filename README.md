<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ورشة الرسم - دروس</title>
    <style>
        /* تحسينات التصميم */
        body { font-family: 'Cairo', sans-serif; background-color: #f3f4f6; margin: 0; padding: 0; }
        .container { max-width: 900px; margin: 20px auto; padding: 20px; background: #fff; border-radius: 10px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); }
        h1 { color: #333; font-size: 26px; }
        .btn { background-color: #1f78b4; color: #fff; padding: 10px 20px; border: none; border-radius: 5px; cursor: pointer; margin: 5px; }
        .btn:hover { background-color: #155a8a; }
        .lesson { margin-bottom: 20px; padding: 15px; background-color: #e9f5fb; border: 1px solid #ddd; border-radius: 8px; }
        .lesson-title { font-size: 20px; font-weight: bold; color: #1f78b4; margin-bottom: 15px; }
        .part { margin-bottom: 10px; padding: 10px; background-color: #fff; border: 1px solid #cfd9e1; border-radius: 5px; position: relative; }
        .copy-btn { position: absolute; right: 10px; top: 10px; background: #007bff; color: white; padding: 5px 10px; border-radius: 4px; cursor: pointer; }
        .copy-btn:hover { background-color: #0056b3; }
        input, textarea { width: calc(100% - 20px); padding: 10px; margin-top: 10px; border-radius: 5px; border: 1px solid #ddd; }
        .add-part-btn { margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>قائمة الدروس</h1>
        <button class="btn" onclick="createLesson()">إنشاء درس جديد</button>
        <div id="lessons"></div>
    </div>

    <script>
        let lessons = [];

        function createLesson() {
            const lessonName = prompt("أدخل اسم الدرس:");
            if (lessonName) {
                const lesson = { name: lessonName, parts: [] };
                lessons.push(lesson);
                renderLessons();
            }
        }

        function addPart(lessonIndex) {
            const partText = prompt("أدخل نص الجزء:");
            const partImage = prompt("أدخل رابط الصورة (اختياري):");
            const partLink = prompt("أدخل رابط (اختياري):");

            const part = {
                text: partText || "",
                image: partImage || "",
                link: partLink || ""
            };

            lessons[lessonIndex].parts.push(part);
            renderLessons();
        }

        function copyText(content) {
            navigator.clipboard.writeText(content).then(() => {
                alert("تم نسخ المحتوى بنجاح!");
            });
        }

        function renderLessons() {
            const lessonsContainer = document.getElementById("lessons");
            lessonsContainer.innerHTML = "";

            lessons.forEach((lesson, index) => {
                const lessonDiv = document.createElement("div");
                lessonDiv.classList.add("lesson");

                const title = document.createElement("div");
                title.classList.add("lesson-title");
                title.textContent = lesson.name;
                lessonDiv.appendChild(title);

                lesson.parts.forEach(part => {
                    const partDiv = document.createElement("div");
                    partDiv.classList.add("part");

                    const partText = document.createElement("p");
                    partText.textContent = part.text;
                    partDiv.appendChild(partText);

                    if (part.image) {
                        const partImage = document.createElement("img");
                        partImage.src = part.image;
                        partImage.alt = "صورة للدرس";
                        partImage.style.maxWidth = "100%";
                        partImage.style.marginTop = "10px";
                        partDiv.appendChild(partImage);
                    }

                    if (part.link) {
                        const partLink = document.createElement("a");
                        partLink.href = part.link;
                        partLink.textContent = "رابط إضافي";
                        partLink.target = "_blank";
                        partLink.style.display = "block";
                        partLink.style.marginTop = "10px";
                        partDiv.appendChild(partLink);
                    }

                    const copyButton = document.createElement("button");
                    copyButton.classList.add("copy-btn");
                    copyButton.textContent = "نسخ المحتوى";
                    copyButton.onclick = () => copyText(part.text);
                    partDiv.appendChild(copyButton);

                    lessonDiv.appendChild(partDiv);
                });

                const addPartButton = document.createElement("button");
                addPartButton.classList.add("btn", "add-part-btn");
                addPartButton.textContent = "إضافة جزء للدرس";
                addPartButton.onclick = () => addPart(index);
                lessonDiv.appendChild(addPartButton);

                lessonsContainer.appendChild(lessonDiv);
            });
        }
    </script>
</body>
</html>
