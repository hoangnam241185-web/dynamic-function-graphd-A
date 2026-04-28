# dynamic-function-graphd-A
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>汽车碰撞吸能对比动态图</title>
    <script src="https://d3js.org/d3.v7.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: #f4f6f8;
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 100%;
            max-width: 900px;
            background: #fff;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
        }
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-bottom: 20px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eee;
        }
        .control-group {
            display: flex;
            align-items: center;
            gap: 10px;
            flex: 1;
            min-width: 250px;
        }
        label {
            font-weight: 500;
            width: 120px;
        }
        input[type="range"] {
            flex: 1;
            cursor: pointer;
        }
        .val-display {
            display: inline-block;
            width: 50px;
            text-align: right;
            font-family: monospace;
            font-size: 14px;
            background: #eee;
            padding: 4px 8px;
            border-radius: 4px;
        }
        svg {
            width: 100%;
            height: auto;
        }
        .axis-label {
            font-size: 14px;
            font-weight: bold;
            fill: #555;
        }
        .grid line {
            stroke: #e0e0e0;
            stroke-dasharray: 2;
        }
        .grid path {
            stroke-width: 0;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="controls">
        <div class="control-group">
            <label>质量 m2 (kg)</label>
            <input type="range" id="m2" min="1" max="10000" value="9941" step="1">
            <span class="val-display" id="m2-val">9941</span>
        </div>
        <div class="control-group">
            <label>速度 v (km/h)</label>
            <input type="range" id="v" min="0" max="300" value="60" step="1">
            <span class="val-display" id="v-val">60</span>
        </div>
        <div class="control-group">
            <label>速度 v3 (km/h)</label>
            <input type="range" id="v3" min="0" max="300" value="120" step="1">
            <span class="val-display" id="v3-val">120</span>
        </div>
    </div>

    <div id="chart"></div>
</div>

<script>
    // 1. 初始化设置
    const width = 860;
    const height = 500;
    const margin = { top: 40, right: 150, bottom: 60, left: 100 }; // 右侧留出图例空间，左侧留出长数字空间
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;

    const svg = d3.select("#chart")
        .append("svg")
        .attr("viewBox", `0 0 ${width} ${height}`);

    const g = svg.append("g")
        .attr("transform", `translate(${margin.left},${margin.top})`);

    // 定义 X 轴和 Y 轴的比例尺
    const xScale = d3.scaleLinear().domain([0, 5000]).range([0, innerWidth]);
    const yScale = d3.scaleLinear().range([innerHeight, 0]);

    // 绘制坐标轴组和网格组
    const xAxisG = g.append("g")
        .attr("transform", `translate(0,${innerHeight})`);
    const yAxisG = g.append("g");
    const gridG = g.append("g").attr("class", "grid");

    // 坐标轴标签
    g.append("text")
        .attr("class", "axis-label")
        .attr("x", innerWidth / 2)
        .attr("y", innerHeight + 45)
        .style("text-anchor", "middle")
        .text("撞击物质量m (kg)");

    g.append("text")
        .attr("class", "axis-label")
        .attr("transform", "rotate(-90)")
        .attr("x", -innerHeight / 2)
        .attr("y", -80)
        .style("text-anchor", "middle")
        .text("单车吸能E（J）");

    // 预先创建线条路径
    const pathCollision = g.append("path")
        .attr("fill", "none")
        .attr("stroke", "#2196F3") // 蓝色
        .attr("stroke-width", 3);

    const pathAsymptote = g.append("path")
        .attr("fill", "none")
        .attr("stroke", "#F44336") // 红色
        .attr("stroke-width", 2)
        .attr("stroke-dasharray", "6,4");

    const pathWall = g.append("path")
        .attr("fill", "none")
        .attr("stroke", "#4CAF50") // 绿色
        .attr("stroke-width", 3);

    // 绘制图例
    const legendData = [
        { label: "对撞：单车吸能", color: "#2196F3", dash: false },
        { label: "渐近线：对撞极限吸能", color: "#F44336", dash: true },
        { label: "撞墙：单车吸能", color: "#4CAF50", dash: false }
    ];

    const legend = svg.append("g")
        .attr("transform", `translate(${width - margin.right + 20}, ${margin.top})`);

    legend.selectAll("line")
        .data(legendData)
        .enter().append("line")
        .attr("x1", 0)
        .attr("x2", 20)
        .attr("y1", (d, i) => i * 30)
        .attr("y2", (d, i) => i * 30)
        .attr("stroke", d => d.color)
        .attr("stroke-width", 3)
        .attr("stroke-dasharray", d => d.dash ? "4,4" : "none");

    legend.selectAll("text")
        .data(legendData)
        .enter().append("text")
        .attr("x", 30)
        .attr("y", (d, i) => i * 30 + 5)
        .text(d => d.label)
        .style("font-size", "12px")
        .style("font-weight", "bold")
        .style("fill", "#555");

    // 2. 核心更新函数
    function updateChart() {
        // 获取控件值
        const m2 = +document.getElementById("m2").value;
        const v_kmh = +document.getElementById("v").value;
        const v3_kmh = +document.getElementById("v3").value;

        // 更新显示数值
        document.getElementById("m2-val").textContent = m2;
        document.getElementById("v-val").textContent = v_kmh;
        document.getElementById("v3-val").textContent = v3_kmh;

        // 速度单位换算 (km/h -> m/s)
        const v_ms = v_kmh / 3.6;
        const v3_ms = v3_kmh / 3.6;

        // 生成 X 轴数据点 (0 到 5000)
        const xData = d3.range(0, 5001, 50);

        // 计算曲线数据
        const dataCollision = xData.map(x => ({
            x: x,
            y: (x * m2 / (x + m2)) * Math.pow(v_ms, 2)
        }));

        const dataWall = xData.map(x => ({
            x: x,
            y: 0.5 * x * Math.pow(v3_ms, 2)
        }));

        // 计算极值用于动态调整 Y 轴
        const maxAsymptote = m2 * Math.pow(v_ms, 2);
        const maxWall = 0.5 * 5000 * Math.pow(v3_ms, 2); // 撞墙在 x=5000 时的值
        const maxY = Math.max(maxAsymptote, maxWall);

        // 更新 Y 轴比例尺 (留出10%顶部边距)
        yScale.domain([0, maxY * 1.1]);

        // 定义线条生成器
        const lineGen = d3.line()
            .x(d => xScale(d.x))
            .y(d => yScale(d.y));

        // 绘制坐标轴 (Y轴强制纯数字格式化，不用缩写)
        xAxisG.call(d3.axisBottom(xScale));
        yAxisG.call(d3.axisLeft(yScale).tickFormat(d3.format("d"))); // "d" 代表纯整数显示

        // 绘制水平网格线
        gridG.call(d3.axisLeft(yScale)
            .tickSize(-innerWidth)
            .tickFormat("")
        );

        // 更新曲线路径
        pathCollision.datum(dataCollision).attr("d", lineGen);
        pathWall.datum(dataWall).attr("d", lineGen);

        // 更新渐近线路径
        pathAsymptote.datum([
            { x: 0, y: maxAsymptote },
            { x: 5000, y: maxAsymptote }
        ]).attr("d", lineGen);
    }

    // 3. 绑定事件监听器
    d3.select("#m2").on("input", updateChart);
    d3.select("#v").on("input", updateChart);
    d3.select("#v3").on("input", updateChart);

    // 初始化渲染
    updateChart();
</script>
</body>
</html>
