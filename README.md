<script>
    const questions = [
        {
            question: "What does the 'A' in SOSTAC® stand for?",
            options: ["Actions", "Analysis", "Advertising", "Alignment"],
            correct: 0
        },
        {
            question: "Which of the following is an example of a SMART campaign objective?",
            options: [
                "Increase website traffic by 50% in six months.",
                "Get more customers.",
                "Boost brand awareness significantly.",
                "Launch a social media campaign."
            ],
            correct: 0
        },
        {
            question: "Which tool is best suited for integrating online and offline campaigns?",
            options: ["SEO", "Social Media Advertising", "Event Sponsorship", "Direct Mail"],
            correct: 1
        },
        {
            question: "In the SOSTAC® framework, what does 'Control' refer to?",
            options: [
                "Evaluating campaign success and metrics.",
                "Creating campaign objectives.",
                "Determining target audiences.",
                "Implementing tactical plans."
            ],
            correct: 0
        }
    ];

    let currentQuestionIndex = 0;
    let score = 0;

    const quizContainer = document.getElementById("quiz");
    const scoreContainer = document.getElementById("score");
    const restartButton = document.getElementById("restart");

    function showQuestion() {
        const questionData = questions[currentQuestionIndex];
        quizContainer.innerHTML = `
            <div class="question">
                <h2>${questionData.question}</h2>
                <div class="options">
                    ${questionData.options
                        .map(
                            (option, index) => `
                            <button onclick="checkAnswer(${index})">${option}</button>
                        `
                        )
                        .join("")}
                </div>
            </div>
        `;
    }

    function checkAnswer(selected) {
        const questionData = questions[currentQuestionIndex];
        const buttons = quizContainer.querySelectorAll("button");

        buttons.forEach((button, index) => {
            if (index === questionData.correct) {
                button.classList.add("correct");
            } else if (index === selected) {
                button.classList.add("wrong");
            }
            button.disabled = true;
        });

        if (selected === questionData.correct) {
            score++;
        }

        currentQuestionIndex++;
        if (currentQuestionIndex < questions.length) {
            setTimeout(showQuestion, 1000);
        } else {
            showScore();
        }
    }

    function showScore() {
        quizContainer.innerHTML = "";
        scoreContainer.textContent = `You scored ${score} out of ${questions.length}.`;
        restartButton.style.display = "block";
    }

    restartButton.addEventListener("click", () => {
        currentQuestionIndex = 0;
        score = 0;
        scoreContainer.textContent = "";
        restartButton.style.display = "none";
        showQuestion();
    });

    showQuestion();
</script>
