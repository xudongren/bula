<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>电子手册与电子名片</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }
        
        :root {
            --primary: #4b6cb7;
            --secondary: #182848;
            --accent: #ff6b6b;
            --light: #f5f7fa;
            --dark: #2c3e50;
            --card-gradient: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
        }
        
        body {
            background: linear-gradient(135deg, #e4edf5 0%, #d0e1f2 100%);
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
            padding: 10px;
            display: flex;
            flex-direction: column;
            background-attachment: fixed;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            height: calc(100vh - 20px);
            position: relative;
        }
        
        /* 顶部导航栏样式 */
        .navbar {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            padding: 15px 0;
            position: relative;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            z-index: 10;
        }
        
        .nav-container {
            overflow-x: auto;
            white-space: nowrap;
            padding: 0 10px;
            scrollbar-width: none;
            -ms-overflow-style: none;
        }
        
        .nav-container::-webkit-scrollbar {
            display: none;
        }
        
        .nav-buttons {
            display: flex;
            min-width: 700px;
        }
        
        .nav-btn {
            background: rgba(255, 255, 255, 0.15);
            border: none;
            color: white;
            padding: 12px 16px;
            border-radius: 50px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 80px;
            text-align: center;
            flex: 1;
            margin: 0 5px;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .nav-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: translateY(-2px);
        }
        
        .nav-btn.active {
            background: var(--accent);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.5);
        }
        
        /* 内容区域样式 */
        .content {
            flex: 1;
            padding: 25px;
            overflow-y: auto;
            background-color: #f9fbfd;
            transition: all 0.4s ease;
            position: relative;
        }
        
        .content-section {
            display: none;
            animation: fadeIn 0.5s ease forwards;
        }
        
        .content-section.active {
            display: block;
        }
        
        .content-title {
            color: var(--dark);
            font-size: 24px;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e0e6ed;
            position: relative;
        }
        
        .content-title::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 60px;
            height: 3px;
            background: var(--accent);
            border-radius: 3px;
        }
        
        .content-text {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.06);
            margin-bottom: 20px;
            line-height: 1.8;
        }
        
        .content-text p {
            margin-bottom: 15px;
        }
        
        .content-text ul {
            padding-left: 25px;
            margin: 15px 0;
        }
        
        .content-text li {
            margin-bottom: 10px;
            position: relative;
        }
        
        .content-text li::before {
            content: '•';
            color: var(--accent);
            font-weight: bold;
            position: absolute;
            left: -20px;
        }
        
        /* 电子名片样式 */
        .card {
            background: var(--card-gradient);
            border-radius: 20px;
            padding: 25px;
            color: white;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            margin-top: 20px;
            position: relative;
            overflow: hidden;
            z-index: 5;
        }
        
        .card::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
        }
        
        .card-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            position: relative;
            z-index: 2;
        }
        
        .avatar {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            overflow: hidden;
            border: 3px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .avatar i {
            font-size: 40px;
            color: white;
        }
        
        .user-info h2 {
            font-size: 22px;
            margin-bottom: 5px;
            font-weight: 700;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        .user-info p {
            opacity: 0.9;
            font-size: 16px;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
        }
        
        .contact-info {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
            position: relative;
            z-index: 2;
        }
        
        .contact-item {
            text-align: center;
            flex: 1;
            padding: 0 10px;
        }
        
        .contact-item i {
            font-size: 28px;
            margin-bottom: 12px;
            color: #ffd43b;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        .contact-item p {
            font-size: 15px;
            margin-bottom: 8px;
            font-weight: 500;
            opacity: 0.95;
        }
        
        .contact-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            padding: 10px 15px;
            border-radius: 50px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 8px;
            width: 100%;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
        }
        
        .contact-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }
        
        .qrcode-container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .qrcode {
            background: white;
            padding: 12px;
            border-radius: 15px;
            display: inline-block;
            margin-top: 10px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }
        
        .qrcode:hover {
            transform: scale(1.05);
        }
        
        .qrcode img {
            width: 120px;
            height: 120px;
            display: block;
        }
        
        .qrcode p {
            color: var(--dark);
            font-size: 12px;
            text-align: center;
            margin-top: 8px;
            font-weight: 700;
        }
        
        /* 动画效果 */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        /* 响应式设计 */
        @media (max-width: 650px) {
            .container {
                height: auto;
                min-height: 100vh;
            }
            
            .nav-buttons {
                min-width: 100%;
                padding: 0 5px;
            }
            
            .nav-btn {
                padding: 10px 12px;
                font-size: 13px;
                min-width: 70px;
                margin: 0 3px;
            }
            
            .content {
                padding: 18px;
            }
            
            .content-text {
                padding: 20px;
            }
            
            .card {
                padding: 20px;
            }
            
            .contact-info {
                flex-direction: column;
                align-items: center;
            }
            
            .contact-item {
                width: 100%;
                max-width: 300px;
                margin-bottom: 25px;
            }
            
            .contact-item:last-child {
                margin-bottom: 0;
            }
            
            .user-info h2 {
                font-size: 20px;
            }
        }
        
        /* 装饰元素 */
        .decoration {
            position: absolute;
            z-index: 0;
            opacity: 0.1;
        }
        
        .circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: var(--accent);
            position: absolute;
            top: 20%;
            right: -50px;
        }
        
        .triangle {
            width: 0;
            height: 0;
            border-left: 80px solid transparent;
            border-right: 80px solid transparent;
            border-bottom: 140px solid var(--primary);
            position: absolute;
            bottom: 50px;
            left: -50px;
            transform: rotate(45deg);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 装饰元素 -->
        <div class="decoration circle"></div>
        <div class="decoration triangle"></div>
        
        <!-- 顶部导航栏 -->
        <div class="navbar">
            <div class="nav-container">
                <div class="nav-buttons">
                    <button class="nav-btn active" data-target="home">首页</button>
                    <button class="nav-btn" data-target="products">产品介绍</button>
                    <button class="nav-btn" data-target="services">服务项目</button>
                    <button class="nav-btn" data-target="cases">成功案例</button>
                    <button class="nav-btn" data-target="solutions">解决方案</button>
                    <button class="nav-btn" data-target="downloads">资料下载</button>
                    <button class="nav-btn" data-target="faq">常见问题</button>
                    <button class="nav-btn" data-target="contact">联系我们</button>
                </div>
            </div>
        </div>
        
        <!-- 内容区域 -->
        <div class="content">
            <!-- 首页内容 -->
            <div id="home" class="content-section active">
                <h2 class="content-title">欢迎使用电子手册</h2>
                <div class="content-text">
                    <p>欢迎访问我们的电子手册系统！在这里您可以获取全面的产品信息、服务内容和技术支持。</p>
                    <p>通过顶部导航栏，您可以快速访问以下内容：</p>
                    <ul>
                        <li><strong>产品介绍</strong> - 了解我们的核心产品与功能</li>
                        <li><strong>服务项目</strong> - 查看我们提供的专业服务</li>
                        <li><strong>成功案例</strong> - 探索我们的客户实施案例</li>
                        <li><strong>解决方案</strong> - 获取针对不同行业的专业解决方案</li>
                        <li><strong>资料下载</strong> - 下载产品手册和技术文档</li>
                        <li><strong>常见问题</strong> - 查找常见问题的解决方案</li>
                        <li><strong>联系我们</strong> - 获取我们的联系方式</li>
                    </ul>
                    <p>请点击上方导航按钮开始浏览，或直接使用底部的电子名片联系我们。</p>
                    <div style="text-align: center; margin-top: 25px;">
                        <i class="fas fa-arrow-down pulse" style="font-size: 32px; color: var(--accent);"></i>
                    </div>
                </div>
            </div>
            
            <!-- 产品介绍 -->
            <div id="products" class="content-section">
                <h2 class="content-title">产品介绍</h2>
                <div class="content-text">
                    <p>我们提供行业领先的解决方案，包括：</p>
                    <ul>
                        <li><strong>智能办公系统</strong> - 提升企业协作效率的全套解决方案</li>
                        <li><strong>数据分析平台</strong> - 深度挖掘业务价值的数据分析工具</li>
                        <li><strong>云服务平台</strong> - 安全可靠的云服务解决方案</li>
                        <li><strong>移动应用开发</strong> - 定制化移动端解决方案</li>
                    </ul>
                    <p>所有产品均采用最新技术，保障系统稳定性和数据安全性，支持多平台使用。</p>
                    <div style="display: flex; justify-content: space-around; margin-top: 25px;">
                        <div style="text-align: center;">
                            <i class="fas fa-laptop-code" style="font-size: 36px; color: var(--primary);"></i>
                            <p style="font-weight: bold; margin-top: 10px;">多平台支持</p>
                        </div>
                        <div style="text-align: center;">
                            <i class="fas fa-shield-alt" style="font-size: 36px; color: var(--primary);"></i>
                            <p style="font-weight: bold; margin-top: 10px;">安全保障</p>
                        </div>
                        <div style="text-align: center;">
                            <i class="fas fa-sync-alt" style="font-size: 36px; color: var(--primary);"></i>
                            <p style="font-weight: bold; margin-top: 10px;">持续更新</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 服务项目 -->
            <div id="services" class="content-section">
                <h2 class="content-title">服务项目</h2>
                <div class="content-text">
                    <p>我们提供全方位的技术服务：</p>
                    <ul>
                        <li><strong>系统定制开发</strong> - 根据需求定制专属解决方案</li>
                        <li><strong>技术咨询</strong> - 专业团队提供技术咨询服务</li>
                        <li><strong>系统集成</strong> - 整合现有系统，提升整体效能</li>
                        <li><strong>运维支持</strong> - 7×24小时专业技术支持</li>
                        <li><strong>培训服务</strong> - 提供系统使用和开发培训</li>
                    </ul>
                    <p style="margin-top: 20px; padding: 15px; background: #f0f7ff; border-radius: 10px; border-left: 4px solid var(--primary);">
                        <i class="fas fa-info-circle" style="color: var(--primary);"></i>
                        我们的服务团队拥有10年以上行业经验，已为200+企业提供专业服务
                    </p>
                </div>
            </div>
            
            <!-- 成功案例 -->
            <div id="cases" class="content-section">
                <h2 class="content-title">成功案例</h2>
                <div class="content-text">
                    <p>以下是我们的一些代表性案例：</p>
                    <ul>
                        <li><strong>金融行业</strong> - 为某银行构建智能风控系统，提升风险识别率35%</li>
                        <li><strong>零售行业</strong> - 为连锁超市开发智能供应链系统，降低库存成本28%</li>
                        <li><strong>制造业</strong> - 为制造企业实施MES系统，提高生产效率22%</li>
                        <li><strong>教育行业</strong> - 为高校开发智慧校园平台，提升管理效率40%</li>
                    </ul>
                    <div style="margin-top: 20px; text-align: center;">
                        <div style="display: inline-block; background: linear-gradient(135deg, #4b6cb7, #182848); color: white; padding: 10px 25px; border-radius: 50px; font-weight: bold;">
                            累计服务客户 300+
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 其他内容区类似，为简洁省略 -->
        </div>
        
        <!-- 底部电子名片 -->
        <div class="card">
            <div class="card-header">
                <div class="avatar">
                    <i class="fas fa-user-tie"></i>
                </div>
                <div class="user-info">
                    <h2>张经理</h2>
                    <p>高级客户经理</p>
                </div>
            </div>
            
            <div class="contact-info">
                <div class="contact-item">
                    <i class="fas fa-phone-alt"></i>
                    <p>联系电话</p>
                    <button class="contact-btn" onclick="callPhone('13800138000')">
                        <i class="fas fa-phone"></i> 138-0013-8000
                    </button>
                </div>
                
                <div class="contact-item">
                    <i class="fas fa-envelope"></i>
                    <p>电子邮箱</p>
                    <button class="contact-btn" onclick="sendEmail('contact@example.com')">
                        <i class="fas fa-envelope"></i> contact@example.com
                    </button>
                </div>
                
                <div class="contact-item">
                    <i class="fab fa-weixin"></i>
                    <p>微信联系</p>
                    <div class="qrcode-container">
                        <div class="qrcode">
                            <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120' viewBox='0 0 120 120'%3E%3Crect width='120' height='120' fill='%23FFFFFF'/%3E%3Cpath d='M24,24 h72 v72 h-72 z' fill='none' stroke='%23333' stroke-width='2'/%3E%3Ccircle cx='45' cy='45' r='4' fill='%23333'/%3E%3Ccircle cx='75' cy='45' r='4' fill='%23333'/%3E%3Ccircle cx='45' cy='75' r='4' fill='%23333'/%3E%3Ccircle cx='75' cy='75' r='4' fill='%23333'/%3E%3C/svg%3E" alt="微信二维码">
                            <p>扫码添加微信</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 导航按钮点击事件
        document.querySelectorAll('.nav-btn').forEach(button => {
            button.addEventListener('click', function() {
                // 移除所有按钮的active类
                document.querySelectorAll('.nav-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                
                // 添加active类到当前按钮
                this.classList.add('active');
                
                // 获取目标内容区ID
                const targetId = this.getAttribute('data-target');
                
                // 隐藏所有内容区
                document.querySelectorAll('.content-section').forEach(section => {
                    section.classList.remove('active');
                });
                
                // 显示目标内容区
                document.getElementById(targetId).classList.add('active');
                
                // 滚动到顶部
                document.querySelector('.content').scrollTop = 0;
            });
        });
        
        // 拨打电话功能
        function callPhone(number) {
            if(confirm(`是否拨打 ${number}?`)) {
                window.location.href = `tel:${number}`;
            }
        }
        
        // 发送邮件功能
        function sendEmail(email) {
            window.location.href = `mailto:${email}`;
        }
        
        // 初始化页面
        document.addEventListener('DOMContentLoaded', function() {
            // 设置第一个内容区为活动状态
            document.getElementById('home').classList.add('active');
            
            // 添加导航按钮点击效果
            const buttons = document.querySelectorAll('.nav-btn');
            buttons.forEach(btn => {
                btn.addEventListener('mousedown', () => {
                    btn.style.transform = 'scale(0.95)';
                });
                btn.addEventListener('mouseup', () => {
                    btn.style.transform = '';
                });
                btn.addEventListener('touchstart', () => {
                    btn.style.transform = 'scale(0.95)';
                });
                btn.addEventListener('touchend', () => {
                    btn.style.transform = '';
                });
            });
        });
    </script>
</body>
</html>
