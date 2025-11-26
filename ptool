<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>パチンコ詳細計算ツール</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Helvetica Neue', Arial, sans-serif;
        }
        
        body {
            background-color: #f0f0f5;
            color: #333;
            line-height: 1.6;
            padding: 0;
            margin: 0;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 15px;
        }
        
        .section {
            background-color: white;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .section-title {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 15px;
            color: #333;
            padding-bottom: 8px;
            border-bottom: 1px solid #eee;
        }
        
        .form-group {
            display: flex;
            align-items: center;
            margin-bottom: 12px;
        }
        
        .form-label {
            width: 100px;
            font-size: 14px;
            font-weight: 500;
        }
        
        .form-input {
            flex: 1;
            height: 36px;
            padding: 0 10px;
            border: 1px solid #cccccc;
            border-radius: 5px;
            font-size: 12px;
            background-color: white;
        }
        
        .form-input:focus {
            outline: none;
            border-color: #4CAF50;
        }
        
        .form-input:disabled {
            background-color: #f5f5f5;
            color: #666666;
        }
        
        .button-group {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .btn {
            flex: 1;
            height: 44px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .btn-save {
            background-color: #4CAF50;
        }
        
        .btn-save:hover {
            background-color: #45a049;
        }
        
        .btn-load {
            background-color: #2196F3;
        }
        
        .btn-load:hover {
            background-color: #0b7dda;
        }
        
        .btn-add {
            background-color: #FF9800;
        }
        
        .btn-add:hover {
            background-color: #e68900;
        }
        
        .result-box {
            text-align: center;
            padding: 20px;
            border-radius: 10px;
            border: 2px solid #dddddd;
            background-color: white;
            margin-top: 15px;
            font-size: 20px;
            font-weight: bold;
        }
        
        .positive {
            color: #008000;
        }
        
        .negative {
            color: #FF4500;
        }
        
        .neutral {
            color: #666666;
        }
        
        .hit-data-container {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            padding: 10px;
            background-color: #f9f9f9;
            border-radius: 5px;
        }
        
        .hit-field {
            flex: 1;
        }
        
        .ratio-display {
            background-color: #ffe8e8;
            text-align: center;
            font-weight: bold;
            font-size: 14px;
            color: #000000;
        }
        
        .ratio-good {
            background-color: #e8ffe8;
        }
        
        .ratio-medium {
            background-color: #fff8e8;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 機種データセクション -->
        <div class="section">
            <div class="section-title">機種データ</div>
            
            <div class="form-group">
                <label class="form-label">交換率</label>
                <input type="text" class="form-input" id="exchange_rate_input" placeholder="3.63" value="3.63">
            </div>
            
            <div class="form-group">
                <label class="form-label">トータル確率</label>
                <input type="text" class="form-input" id="probability_input" placeholder="9.5" value="9.5">
            </div>
            
            <div class="form-group">
                <label class="form-label">渡玉</label>
                <input type="text" class="form-input" id="given_balls_input" placeholder="玉数">
            </div>
            
            <div class="form-group">
                <label class="form-label">受玉</label>
                <input type="text" class="form-input" id="received_balls_input" placeholder="玉数">
            </div>
            
            <div class="form-group">
                <label class="form-label">現金投資</label>
                <input type="text" class="form-input" id="cash_input" placeholder="玉数">
            </div>
            
            <div class="form-group">
                <label class="form-label">貯玉投資</label>
                <input type="text" class="form-input" id="ball_investment_input" placeholder="玉数">
            </div>
            
            <div class="form-group">
                <label class="form-label">持ち玉</label>
                <input type="text" class="form-input" id="owned_balls_input" placeholder="玉数">
            </div>
            
            <div class="form-group">
                <label class="form-label">持玉比率</label>
                <input type="text" class="form-input ratio-display" id="ball_ratio_label" placeholder="○%">
            </div>
        </div>
        
        <!-- データ管理セクション -->
        <div class="section">
            <div class="section-title">データ管理</div>
            
            <div class="button-group">
                <button class="btn btn-save" id="save_button">データ保存</button>
                <button class="btn btn-load" id="load_button">データ読み込み</button>
            </div>
        </div>
        
        <!-- 初当りデータセクション -->
        <div class="section">
            <div class="section-title">初当りデータ</div>
            
            <button class="btn btn-add" id="start_button">データを追加</button>
            
            <div id="hit_data_container">
                <!-- 初当りデータがここに動的に追加されます -->
            </div>
        </div>
        
        <!-- 仕事量計算セクション -->
        <div class="section">
            <div class="section-title">仕事量計算</div>
            
            <div class="form-group">
                <label class="form-label">通常回転数</label>
                <input type="text" class="form-input" id="rotation_input" value="0" disabled>
            </div>
            
            <div class="form-group">
                <label class="form-label">回転率</label>
                <input type="text" class="form-input" id="rate_input" value="0.00" disabled>
            </div>
            
            <div class="form-group">
                <label class="form-label">等価ボーダー</label>
                <input type="text" class="form-input" id="border_input" value="0.00" disabled>
            </div>
            
            <div class="form-group">
                <label class="form-label">持ち玉単価</label>
                <input type="text" class="form-input" id="unit_price_input" value="0.00" disabled>
            </div>
            
            <div class="form-group">
                <label class="form-label">現金単価</label>
                <input type="text" class="form-input" id="cash_unit_price_input" value="0.00" disabled>
            </div>
            
            <div class="form-group">
                <label class="form-label">1R出玉</label>
                <input type="text" class="form-input" id="ball_per_round_input" value="0.00" disabled>
            </div>
            
            <div class="result-box" id="result_label">
                仕事量: 計算可能
            </div>
            
            <div class="result-box" id="profit_label">
                収支: 計算可能
            </div>
        </div>
    </div>

    <script>
        // グローバル変数
        let firstHitCount = 0;
        let firstHitFields = [];
        
        // データ保存用のキー
        const DATA_KEY = 'pachinko_data';
        
        // DOMの読み込み完了後に実行
        document.addEventListener('DOMContentLoaded', function() {
            // イベントリスナーの設定
            setupEventListeners();
            
            // 初期計算を実行
            calculateAll();
        });
        
        // イベントリスナーの設定
        function setupEventListeners() {
            // 機種データ入力フィールド
            const machineFields = [
                'exchange_rate_input', 'probability_input', 'given_balls_input',
                'received_balls_input', 'cash_input', 'ball_investment_input',
                'owned_balls_input', 'ball_ratio_label'
            ];
            
            machineFields.forEach(fieldId => {
                const field = document.getElementById(fieldId);
                if (field) {
                    field.addEventListener('input', calculateAll);
                    field.addEventListener('blur', calculateAll);
                }
            });
            
            // ボタン
            document.getElementById('save_button').addEventListener('click', saveData);
            document.getElementById('load_button').addEventListener('click', loadData);
            document.getElementById('start_button').addEventListener('click', addFirstHitFields);
            
            // 背景タップでキーボードを閉じる
            document.body.addEventListener('click', function(e) {
                if (e.target.tagName !== 'INPUT') {
                    closeKeyboard();
                }
            });
        }
        
        // キーボードを閉じる
        function closeKeyboard() {
            document.activeElement.blur();
        }
        
        // データ保存関数
        function saveData() {
            const data = {
                firstHitCount: firstHitCount,
                firstHitData: {},
                machineData: {}
            };
            
            // 機種データを保存
            const machineFields = [
                'exchange_rate_input', 'probability_input', 'given_balls_input',
                'received_balls_input', 'cash_input', 'ball_investment_input',
                'owned_balls_input', 'ball_ratio_label'
            ];
            
            machineFields.forEach(fieldId => {
                const field = document.getElementById(fieldId);
                if (field) {
                    data.machineData[fieldId] = field.value || '';
                }
            });
            
            // 初当りデータを保存
            for (let i = 1; i <= firstHitCount; i++) {
                const fieldSetId = `hit_${i}`;
                const hitData = {};
                
                const rotationField = document.getElementById(`${fieldSetId}_rotation`);
                const ballsField = document.getElementById(`${fieldSetId}_balls`);
                const roundsField = document.getElementById(`${fieldSetId}_rounds`);
                const timeField = document.getElementById(`${fieldSetId}_time`);
                
                if (rotationField) hitData.rotation = rotationField.value || '';
                if (ballsField) hitData.balls = ballsField.value || '';
                if (roundsField) hitData.rounds = roundsField.value || '';
                if (timeField) hitData.time = timeField.value || '';
                
                data.firstHitData[fieldSetId] = hitData;
            }
            
            // ローカルストレージに保存
            try {
                localStorage.setItem(DATA_KEY, JSON.stringify(data));
                showMessage('データを保存しました');
            } catch (e) {
                showMessage('データ保存エラー: ' + e.message);
            }
        }
        
        // データ読み込み関数
        function loadData() {
            try {
                const dataStr = localStorage.getItem(DATA_KEY);
                if (!dataStr) {
                    showMessage('保存されたデータがありません');
                    return;
                }
                
                const data = JSON.parse(dataStr);
                
                // 機種データを復元
                if (data.machineData) {
                    Object.keys(data.machineData).forEach(fieldId => {
                        const field = document.getElementById(fieldId);
                        if (field) {
                            field.value = data.machineData[fieldId];
                        }
                    });
                }
                
                // 初当りデータを復元
                const savedHitCount = data.firstHitCount || 0;
                const firstHitData = data.firstHitData || {};
                
                // 既存の初当りデータをクリア
                const hitDataContainer = document.getElementById('hit_data_container');
                hitDataContainer.innerHTML = '';
                firstHitCount = 0;
                firstHitFields = [];
                
                // 必要な分だけフィールドを追加
                for (let i = 1; i <= savedHitCount; i++) {
                    addFirstHitFields();
                    
                    const fieldSetId = `hit_${i}`;
                    if (firstHitData[fieldSetId]) {
                        const hitData = firstHitData[fieldSetId];
                        
                        const rotationField = document.getElementById(`${fieldSetId}_rotation`);
                        const ballsField = document.getElementById(`${fieldSetId}_balls`);
                        const roundsField = document.getElementById(`${fieldSetId}_rounds`);
                        const timeField = document.getElementById(`${fieldSetId}_time`);
                        
                        if (rotationField && hitData.rotation) rotationField.value = hitData.rotation;
                        if (ballsField && hitData.balls) ballsField.value = hitData.balls;
                        if (roundsField && hitData.rounds) roundsField.value = hitData.rounds;
                        if (timeField && hitData.time) timeField.value = hitData.time;
                    }
                }
                
                showMessage('データを読み込みました');
                calculateAll();
                
            } catch (e) {
                showMessage('データ読み込みエラー: ' + e.message);
            }
        }
        
        // メッセージ表示
        function showMessage(message) {
            alert(message);
        }
        
        // 初当りデータ入力フォームの追加
        function addFirstHitFields() {
            firstHitCount++;
            const fieldSetId = `hit_${firstHitCount}`;
            
            const hitDataContainer = document.getElementById('hit_data_container');
            
            const fieldContainer = document.createElement('div');
            fieldContainer.className = 'hit-data-container';
            fieldContainer.id = `${fieldSetId}_container`;
            
            // 回転数フィールド
            const rotationField = createTextField(fieldSetId, 'rotation', '回転数');
            fieldContainer.appendChild(rotationField);
            
            // 出玉フィールド
            const ballsField = createTextField(fieldSetId, 'balls', '出玉');
            fieldContainer.appendChild(ballsField);
            
            // ラウンドフィールド
            const roundsField = createTextField(fieldSetId, 'rounds', 'ラウンド');
            fieldContainer.appendChild(roundsField);
            
            // 時短フィールド
            const timeField = createTextField(fieldSetId, 'time', '時短');
            fieldContainer.appendChild(timeField);
            
            hitDataContainer.appendChild(fieldContainer);
            firstHitFields.push(fieldSetId);
            
            // 計算を更新
            calculateAll();
        }
        
        // テキストフィールド作成ヘルパー
        function createTextField(fieldSetId, fieldType, placeholder) {
            const container = document.createElement('div');
            container.className = 'hit-field';
            
            const input = document.createElement('input');
            input.type = 'text';
            input.className = 'form-input';
            input.id = `${fieldSetId}_${fieldType}`;
            input.placeholder = placeholder;
            
            input.addEventListener('input', calculateAll);
            input.addEventListener('blur', calculateAll);
            
            container.appendChild(input);
            return container;
        }
        
        // 仕事量計算
        function calculateJobAmount(totalRotation, ballRatio, ownedUnitPrice, cashUnitPrice) {
            try {
                const T = parseFloat(totalRotation);
                const ratio = ballRatio ? parseFloat(ballRatio) : 0;
                const ownedUnit = parseFloat(ownedUnitPrice);
                const cashUnit = parseFloat(cashUnitPrice);
                
                // 仕事量 = 総回転数 × (持ち玉比率/100) × 持ち玉単価 + 総回転数 × (1 - (持ち玉比率/100)) × 現金単価
                const ownedPart = T * (ratio / 100) * ownedUnit;
                const cashPart = T * (1 - (ratio / 100)) * cashUnit;
                const jobAmount = ownedPart + cashPart;
                
                return jobAmount;
            } catch (e) {
                return null;
            }
        }
        
        // 収支計算
        function calculateProfit(cashInvestment, ballInvestment, ownedBalls, exchangeRate) {
            try {
                const cash = parseFloat(cashInvestment);
                const ballInv = parseFloat(ballInvestment);
                const owned = parseFloat(ownedBalls);
                const rate = parseFloat(exchangeRate);
                
                // 収支 = (持ち玉 - 貯玉投資) * 交換率 - (現金投資 * 4)
                const profit = (owned - ballInv) * rate - (cash * 4);
                return profit;
            } catch (e) {
                return null;
            }
        }
        
        // 持玉比率計算
        function calculateDetailedData(cashInvestment, ballInvestment, ownedBalls) {
            try {
                const cash = parseFloat(cashInvestment);
                const ballInv = parseFloat(ballInvestment);
                const owned = parseFloat(ownedBalls);
                
                // 持ち玉比率計算
                if ((cash + ballInv) > 0) {
                    const ballRatio = (owned / (cash + ballInv)) * 100;
                    return ballRatio;
                } else {
                    return 0;
                }
            } catch (e) {
                return null;
            }
        }
        
        // 等価ボーダーを計算
        function calculateEquivalentBorder(ballPerRound, totalProbability) {
            try {
                if (ballPerRound > 0 && parseFloat(totalProbability) > 0) {
                    // 等価ボーダー = 250 / (1R出玉 / トータル確率)
                    const equivalentBorder = 250 / (ballPerRound / parseFloat(totalProbability));
                    return equivalentBorder;
                } else {
                    return 0;
                }
            } catch (e) {
                return 0;
            }
        }
        
        // 単価を計算
        function calculateUnitPrices(ballPerRound, totalProbability, exchangeRate, actualRate) {
            try {
                if (ballPerRound > 0 && parseFloat(totalProbability) > 0 && 
                    parseFloat(exchangeRate) > 0 && actualRate > 0) {
                    
                    const baseValue = (ballPerRound / parseFloat(totalProbability)) * parseFloat(exchangeRate);
                    
                    // 持ち玉単価 = (1R出玉 / トータル確率) × 交換率 - (250 / 回転率) × 交換率
                    const ownedUnitPrice = baseValue - (250 / actualRate) * parseFloat(exchangeRate);
                    
                    // 現金単価 = (1R出玉 / トータル確率) × 交換率 - (250 / 回転率) × 4
                    const cashUnitPrice = baseValue - (250 / actualRate) * 4;
                    
                    return { ownedUnitPrice, cashUnitPrice };
                } else {
                    return { ownedUnitPrice: 0, cashUnitPrice: 0 };
                }
            } catch (e) {
                return { ownedUnitPrice: 0, cashUnitPrice: 0 };
            }
        }
        
        // 初当りデータから通常回転数を計算
        function calculateTotalRotation() {
            if (firstHitCount === 0) {
                return 0;
            }
            
            let totalRotation = 0;
            let totalTimeShort = 0;
            
            // 各初当りデータフィールドから値を取得して計算
            for (let i = 1; i <= firstHitCount; i++) {
                const fieldSetId = `hit_${i}`;
                
                const rotationField = document.getElementById(`${fieldSetId}_rotation`);
                const timeField = document.getElementById(`${fieldSetId}_time`);
                
                const rotationValue = rotationField && rotationField.value ? rotationField.value : '0';
                const timeValue = timeField && timeField.value ? timeField.value : '0';
                
                try {
                    totalRotation += parseFloat(rotationValue);
                    totalTimeShort += parseFloat(timeValue);
                } catch (e) {
                    // 無効な値は無視
                }
            }
            
            // 通常回転数 = 回転数の合計 - 時短の合計
            const normalRotation = totalRotation - totalTimeShort;
            return Math.max(0, normalRotation);
        }
        
        // 総玉数とラウンド合計を計算
        function calculateTotalBallsAndRounds() {
            // 機種データから値を取得
            const cashInvestment = document.getElementById('cash_input').value || '0';
            const ballInvestment = document.getElementById('ball_investment_input').value || '0';
            const givenBalls = document.getElementById('given_balls_input').value || '0';
            const receivedBalls = document.getElementById('received_balls_input').value || '0';
            const ownedBalls = document.getElementById('owned_balls_input').value || '0';
            
            // 初当りデータから出玉の合計とラウンドの合計を計算
            let totalBallOutput = 0;
            let totalRounds = 0;
            
            for (let i = 1; i <= firstHitCount; i++) {
                const fieldSetId = `hit_${i}`;
                
                const ballsField = document.getElementById(`${fieldSetId}_balls`);
                const roundsField = document.getElementById(`${fieldSetId}_rounds`);
                
                const ballValue = ballsField && ballsField.value ? ballsField.value : '0';
                const roundValue = roundsField && roundsField.value ? roundsField.value : '0';
                
                try {
                    totalBallOutput += parseFloat(ballValue);
                    totalRounds += parseFloat(roundValue);
                } catch (e) {
                    // 無効な値は無視
                }
            }
            
            try {
                // 玉数 = 現金投資 + 貯玉投資 + 受玉 - 渡玉 + (出玉の合計) - 持ち玉
                const cash = parseFloat(cashInvestment);
                const ballInv = parseFloat(ballInvestment);
                const given = parseFloat(givenBalls);
                const received = parseFloat(receivedBalls);
                const owned = parseFloat(ownedBalls);
                
                const totalBalls = cash + ballInv + received - given + totalBallOutput - owned;
                
                // 1R出玉を計算(ラウンド合計が0の場合は0)
                const ballPerRound = totalRounds > 0 ? totalBallOutput / totalRounds : 0;
                
                return {
                    totalBalls: Math.max(0, totalBalls),
                    ballPerRound: ballPerRound
                };
            } catch (e) {
                return {
                    totalBalls: 0,
                    ballPerRound: 0
                };
            }
        }
        
        // 計算実行
        function calculateAll() {
            // 通常回転数を初当りデータから自動計算
            const totalRotation = calculateTotalRotation();
            
            // 通常回転数フィールドを更新
            document.getElementById('rotation_input').value = Math.floor(totalRotation);
            
            // 総玉数と1R出玉を計算
            const { totalBalls, ballPerRound } = calculateTotalBallsAndRounds();
            
            // 回転率計算
            let actualRate = 0;
            if (totalBalls > 0) {
                actualRate = totalRotation / (totalBalls / 250);
            }
            
            // 回転率フィールドを更新
            document.getElementById('rate_input').value = actualRate.toFixed(2);
            
            // 1R出玉フィールドを更新(小数点第2位まで表示)
            document.getElementById('ball_per_round_input').value = ballPerRound.toFixed(2);
            
            // 等価ボーダーを計算
            const totalProbability = document.getElementById('probability_input').value || '0';
            const equivalentBorder = calculateEquivalentBorder(ballPerRound, totalProbability);
            
            // 等価ボーダーフィールドを更新
            document.getElementById('border_input').value = equivalentBorder.toFixed(2);
            
            // 単価を計算
            const exchangeRate = document.getElementById('exchange_rate_input').value || '0';
            const { ownedUnitPrice, cashUnitPrice } = calculateUnitPrices(
                ballPerRound, totalProbability, exchangeRate, actualRate
            );
            
            // 持ち玉単価フィールドを更新
            document.getElementById('unit_price_input').value = ownedUnitPrice.toFixed(2);
            
            // 現金単価フィールドを更新
            document.getElementById('cash_unit_price_input').value = cashUnitPrice.toFixed(2);
            
            // 持ち玉比率を計算と表示を更新
            const cashInvestment = document.getElementById('cash_input').value || '0';
            const ballInvestment = document.getElementById('ball_investment_input').value || '0';
            const ownedBalls = document.getElementById('owned_balls_input').value || '0';
            const ballRatio = calculateDetailedData(cashInvestment, ballInvestment, ownedBalls);
            
            // 持玉比率表示を更新
            const ratioField = document.getElementById('ball_ratio_label');
            if (ballRatio !== null) {
                ratioField.value = ballRatio.toFixed(1) + '%';
                
                // 背景色を比率に応じて変更
                if (ballRatio >= 100) {
                    ratioField.className = 'form-input ratio-display ratio-good';
                } else if (ballRatio > 0) {
                    ratioField.className = 'form-input ratio-display ratio-medium';
                } else {
                    ratioField.className = 'form-input ratio-display';
                }
            }
            
            // 仕事量計算(新しい計算式を使用)
            const jobAmount = calculateJobAmount(
                totalRotation, 
                ballRatio, 
                ownedUnitPrice, 
                cashUnitPrice
            );
            
            // 収支計算を追加
            const profit = calculateProfit(
                cashInvestment, 
                ballInvestment, 
                ownedBalls, 
                exchangeRate
            );
            
            // 結果表示を更新
            const resultLabel = document.getElementById('result_label');
            if (jobAmount !== null) {
                resultLabel.textContent = `仕事量: ¥${jobAmount.toLocaleString()}`;
                resultLabel.className = jobAmount >= 0 ? 'result-box positive' : 'result-box negative';
            } else {
                resultLabel.textContent = "仕事量: 計算可能";
                resultLabel.className = 'result-box neutral';
            }
            
            // 収支表示を更新
            const profitLabel = document.getElementById('profit_label');
            if (profit !== null) {
                profitLabel.textContent = `収支: ¥${profit.toLocaleString()}`;
                profitLabel.className = profit >= 0 ? 'result-box positive' : 'result-box negative';
            } else {
                profitLabel.textContent = "収支: 計算中";
                profitLabel.className = 'result-box neutral';
            }
        }
    </script>
</body>
</html>
