<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* --- 核心设计变量 --- */
        :root {
            --primary-color: #002D62; /* 首尔大学/国际通商 深蓝色 */
            --secondary-color: #FDFDFD; /* 极简白色背景 */
            --accent-color: #E6B400; /* 金色点缀 */
            --text-main: #333333;
            --text-sub: #666666;
            --font-main: 'Helvetica Neue', Helvetica, Arial, PingFang SC, Lantinghei SC, sans-serif;
        }

        /* --- 基础布局 --- */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: var(--font-main); color: var(--text-main); background-color: var(--secondary-color); line-height: 1.8; -webkit-font-smoothing: antialiased; }
        a { text-decoration: none; color: inherit; transition: color 0.3s ease; }
        a:hover { color: var(--accent-color); }
        ul { list-style: none; }

        /* --- 栅格系统 --- */
        .container { max-width: 1080px; margin: 0 auto; padding: 0 40px; }
        @media (max-width: 768px) { .container { padding: 0 20px; } }

        /* --- 导航栏 --- */
        .navbar { background-color: var(--secondary-color); border-bottom: 1px solid #EEE; position: sticky; top: 0; z-index: 1000; padding: 20px 0; }
        .nav-content { display: flex; justify-content: space-between; align-items: center; }
        .nav-logo { font-size: 24px; font-weight: 700; color: var(--primary-color); letter-spacing: 1px; }
        .nav-links { display: flex; gap: 30px; font-size: 15px; text-transform: uppercase; letter-spacing: 1px; }
        @media (max-width: 768px) { .nav-links { display: none; } } /* 手机端简化 */

        /* --- 首页 Hero 区域 (设计感核心) --- */
        .hero { background-color: #FAFAFA; border-bottom: 1px solid #EEE; padding: 120px 0; text-align: center; position: relative; }
        .hero::after { content: ''; position: absolute; bottom: -1px; left: 50%; transform: translateX(-50%); width: 60px; height: 3px; background-color: var(--accent-color); }
        .hero-name { font-size: 56px; font-weight: 900; color: var(--primary-color); letter-spacing: -2px; margin-bottom: 15px; }
        .hero-title { font-size: 18px; color: var(--text-sub); text-transform: uppercase; letter-spacing: 2px; margin-bottom: 30px; }
        .hero-bio { font-size: 20px; color: var(--text-main); max-width: 700px; margin: 0 auto 50px; font-weight: 300; }
        .hero-btns { display: flex; gap: 20px; justify-content: center; }
        .btn { padding: 12px 30px; font-size: 15px; font-weight: 600; text-transform: uppercase; letter-spacing: 1px; border-radius: 4px; transition: all 0.3s ease; }
        .btn-primary { background-color: var(--primary-color); color: #FFF; border: 1px solid var(--primary-color); }
        .btn-primary:hover { background-color: #FFF; color: var(--primary-color); }
        .btn-secondary { background-color: #FFF; color: var(--primary-color); border: 1px solid #DDD; }
        .btn-secondary:hover { border-color: var(--primary-color); }

        /* --- 通用板块设置 --- */
        .section { padding: 90px 0; border-bottom: 1px solid #EEE; }
        .section-title { font-size: 32px; font-weight: 700; color: var(--primary-color); margin-bottom: 60px; text-align: center; position: relative; padding-bottom: 15px; }
        .section-title::after { content: ''; position: absolute; bottom: 0; left: 50%; transform: translateX(-50%); width: 40px; height: 2px; background-color: var(--accent-color); }

        /* --- 教育与经历板块 (时间轴风) --- */
        .exp-item { margin-bottom: 50px; display: grid; grid-template-columns: 220px 1fr; gap: 40px; }
        .exp-date { font-size: 15px; color: var(--text-sub); font-weight: 500; text-transform: uppercase; letter-spacing: 1px; }
        .exp-content { border-left: 2px solid #EEE; padding-left: 40px; }
        .exp-org { font-size: 20px; font-weight: 700; color: var(--primary-color); margin-bottom: 8px; }
        .exp-title { font-size: 17px; font-weight: 600; color: var(--text-main); margin-bottom: 15px; }
        .exp-desc { font-size: 16px; color: var(--text-sub); list-style: disc; margin-left: 20px; }
        @media (max-width: 768px) { .exp-item { grid-template-columns: 1fr; gap: 15px; } .exp-content { border-left: none; padding-left: 0; } }

        /* --- 项目与作品集 (卡片设计) --- */
        .portfolio-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 30px; }
        .card { background: #FFF; border: 1px solid #EEE; border-radius: 8px; overflow: hidden; transition: box-shadow 0.3s ease, transform 0.3s ease; display: flex; flex-direction: column; }
        .card:hover { box-shadow: 0 10px 30px rgba(0,0,0,0.08); transform: translateY(-5px); }
        .card-body { padding: 30px; flex-grow: 1; display: flex; flex-direction: column; }
        .card-tag { font-size: 12px; font-weight: 600; text-transform: uppercase; color: var(--accent-color); letter-spacing: 1px; margin-bottom: 10px; }
        .card-title { font-size: 20px; font-weight: 700; color: var(--primary-color); margin-bottom: 15px; line-height: 1.4; }
        .card-text { font-size: 15px; color: var(--text-sub); margin-bottom: 25px; flex-grow: 1; }
        .card-link { font-size: 14px; font-weight: 600; color: var(--primary-color); text-transform: uppercase; letter-spacing: 1px; }

        /* --- 技能板块 (标签设计) --- */
        .skills-content { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 40px; }
        .skill-group-title { font-size: 18px; font-weight: 600; color: var(--text-main); margin-bottom: 20px; border-bottom: 1px solid #EEE; padding-bottom: 10px; }
        .skill-tags { display: flex; flex-wrap: wrap; gap: 12px; }
        .skill-tag { background-color: #F0F4F8; color: var(--primary-color); padding: 8px 16px; font-size: 14px; border-radius: 20px; font-weight: 500; }

        /* --- 页脚 --- */
        .footer { padding: 60px 0; background-color: #FAFAFA; text-align: center; color: var(--text-sub); border-top: 1px solid #EEE; font-size: 15px; }
        .footer-socials { display: flex; gap: 20px; justify-content: center; margin-bottom: 30px; font-size: 14px; text-transform: uppercase; letter-spacing: 1px; }

    </style>
</head>
<body>

    <!-- 导航栏 -->
    <nav class="navbar">
        <div class="container nav-content">
            <!-- 修改这里：将名字换成你自己的中文名或英文简称 -->
            <div class="nav-logo">YUTONG WANG</div>
            <div class="nav-links">
                <a href="#about">About</a>
                <a href="#education">Education</a>
                <a href="#projects">Projects</a>
                <a href="#skills">Skills</a>
                <a href="#contact">Contact</a>
            </div>
        </div>
    </nav>

    <!-- 首页 Hero 区域 -->
    <header class="hero">
        <div class="container">
            <!-- 修改这里：WANG YUTONG -->
            <h1 class="hero-name">王语彤 (Yutong Wang)</h1>
            <!-- 修改这里：Marketing Analyst -->
            <p class="hero-title">International Commerce | Global Business Strategy | Computational Analytics</p>
            <!-- 👋 Hi, I'm Yutong Wang (Rita) -->
            <p class="hero-bio">Master’s Candidate at Seoul National University (SNU GSIS), specializing in International Commerce and International Business Management. My work bridges qualitative communication theory, digital branding, and quantitative data analysis (Python, NLP).</p>
            <div class="hero-btns">
                <!-- Linkedin:Rita Wang -->
                <a href="https://linkedin.com" class="btn btn-primary" target="_blank">View LinkedIn</a>
                <!-- 修改这里：将这里的链接替换为你存放在仓库中的简历 PDF 网址 -->
                <a href="https://github.com/yutongwang759-code/yutongwang759-code.github.io/raw/main/Resume_YutongWang.pdf" class="btn btn-secondary" target="_blank">Download CV (PDF)</a>
            </div>
        </div>
    </header>

    <!-- 教育背景板块 -->
    <section id="education" class="section">
        <div class="container">
            <h2 class="section-title">Education</h2>
            
            <div class="exp-item">
                <div class="exp-date">Sep 2024 - Present</div>
                <div class="exp-content">
                    <div class="exp-org">Seoul National University (SNU)</div>
                    <div class="exp-title">M.A. Candidate in International Studies (GSIS)</div>
                    <ul class="exp-desc">
                        <li>Major: International Commerce & International Business Management</li>
                    </ul>
                </div>
            </div>

            <div class="exp-item">
                <div class="exp-date">Sep 2020 - Jun 2024</div>
                <div class="exp-content">
                    <div class="exp-org">Soochow University</div>
                    <div class="exp-title">B.A. in Advertising</div>
                    <ul class="exp-desc">
                        <li>GPA: 3.7 / 4.0</li>
                        <li>Academic Excellence Award (2022, 2023)</li>
                    </ul>
                </div>
            </div>

        </div>
    </section>

    <!-- 技能与语言板块 -->
    <section id="skills" class="section">
        <div class="container">
            <h2 class="section-title">Skills & Languages</h2>
            <div class="skills-content">
                
                <div class="skill-group">
                    <h3 class="skill-group-title">Technical & Data</h3>
                    <div class="skill-tags">
                        <span class="skill-tag">Python (Pandas, NLP, Jieba)</span>
                        <span class="skill-tag">SQL</span>
                        <span class="skill-tag">Data Monitoring</span>
                        <span class="skill-tag">Git / GitHub</span>
                    </div>
                </div>

                <div class="skill-group">
                    <h3 class="skill-group-title">Business & PR</h3>
                    <div class="skill-tags">
                        <span class="skill-tag">International Trade</span>
                        <span class="skill-tag">Global Business Strategy</span>
                        <span class="skill-tag">Crisis PR</span>
                        <span class="skill-tag">Influencer Marketing</span>
                    </div>
                </div>

                <div class="skill-group">
                    <h3 class="skill-group-title">Languages</h3>
                    <div class="skill-tags">
                        <span class="skill-tag">Mandarin (Native)</span>
                        <span class="skill-tag">English (IELTS 7.5)</span>
                        <span class="skill-tag">Korean (TOPIK 6)</span>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- 页脚与联系方式 -->
    <footer id="contact" class="footer">
        <div class="container">
            <div class="footer-socials">
                <!-- ritawang0486@snu.ac.kr -->
                <a href="mailto:your_email@example.com">Email</a>
                <!-- (https://github.com/yutongwang759-code) -->
                <a href="https://github.com/yutongwang759-code">GitHub</a>
            </div>
            <p>&copy; 2024 Yutong Wang. All Rights Reserved.</p>
            <p>Master's Candidate in International Studies, SNU GSIS</p>
        </div>
    </footer>

</body>
</html>ive), English (Fluent / IELTS 7.5), Korean (Fluent / TOPIK Level 6)
* **Technical Skills**: Python (Pandas, Jieba, NLTK, WordCloud), SQL, Data Visualization, Social Listening & Monitoring
