<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>복권구매 결제 뱅킹앱 선택</title>
    <style>
        /* 페이퍼로지 폰트 적용 */
        @font-face {
            font-family: 'Paperlogy';
            font-weight: 800;
            src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-8ExtraBold.woff2') format('woff2');
        }
        @font-face {
            font-family: 'Paperlogy';
            font-weight: 500;
            src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2408-3@1.0/Paperlogy-5Medium.woff2') format('woff2');
        }

        body {
            font-family: 'Paperlogy', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f8f9fa;
            display: flex;
            justify-content: center;
        }

        .mobile-container {
            width: 100%;
            max-width: 480px;
            background-color: #ffffff;
            height: 100vh;
            padding: 15px 10px;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
        }

        .header {
            text-align: center;
            margin-bottom: 15px;
        }

        .header h1 {
            font-weight: 800;
            font-size: 1.15rem;
            color: #111;
            margin: 0;
            word-break: keep-all;
        }

        .header h1 span {
            color: #d4af37;
        }

        .bank-container {
            display: flex;
            flex-wrap: wrap;
            margin: -2px;
            flex-grow: 1;
            align-content: flex-start;
        }

        .btn-wrap {
            padding: 2px;
            box-sizing: border-box;
        }

        .w-3 { width: 33.333%; }
        .w-2 { width: 50%; }

        .bank-btn {
            width: 100%;
            height: 100%;
            background-color: #fff;
            border-style: solid;
            border-width: 1.5px;
            border-radius: 8px;
            padding: 6px 2px;
            text-align: center;
            font-family: 'Paperlogy', sans-serif;
            cursor: pointer;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
            -webkit-tap-highlight-color: transparent;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .bank-btn:active {
            transform: scale(0.96);
            background-color: #f9f9f9;
        }

        /* 분류별 테두리 컬러 */
        .border-internet { border-color: #8A2BE2; }
        .border-commercial { border-color: #1E90FF; }
        .border-regional { border-color: #00BF2F; }
        .border-mutual { border-color: #FF7F50; }

        .bank-name {
            font-size: 0.6rem;
            color: #777;
            margin-bottom: 2px;
            font-weight: 500;
        }
        
        .app-name {
            font-size: 0.75rem;
            font-weight: 800;
            color: #222;
        }

        /* --- 모달(팝업창) 스타일 --- */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.6);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
            box-sizing: border-box;
        }

        .modal-content {
            background-color: #fff;
            padding: 25px 20px;
            border-radius: 12px;
            width: 100%;
            max-width: 320px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        .modal-text {
            font-family: 'Paperlogy', sans-serif;
            font-weight: 500;
            font-size: 1rem;
            line-height: 1.5;
            color: #333;
            margin-top: 0;
            margin-bottom: 20px;
            word-break: keep-all;
        }

        .account-highlight {
            display: block;
            color: #d4af37;
            font-weight: 800;
            font-size: 1.2rem;
            margin: 10px 0;
        }

        .confirm-btn {
            background-color: #d4af37;
            border: none;
            border-radius: 8px;
            padding: 15px 0;
            font-family: 'Paperlogy', sans-serif;
            font-weight: 800;
            font-size: 1.1rem;
            color: #fff;
            cursor: pointer;
            width: 100%;
            box-shadow: 0 4px 6px rgba(212, 175, 55, 0.3);
            transition: all 0.2s ease;
            display: block;
            text-decoration: none;
            box-sizing: border-box;
        }

        .confirm-btn:active {
            background-color: #b8962c;
            transform: scale(0.97);
        }
    </style>
</head>
<body>

<div class="mobile-container">
    <div class="header">
        <h1>송금에 사용할 내 <span>뱅킹앱</span>을 선택하세요</h1>
    </div>

    <!-- 뱅킹앱 리스트 (정확한 최신 Scheme 및 Package 교체 완료) -->
    <div class="bank-container">
        <!-- 1. 인터넷전문은행 -->
        <div class="btn-wrap w-3"><button class="bank-btn border-internet" onclick="prepareTransfer('kakaobank://', 'com.kakaobank.channel')"><span class="bank-name">카카오뱅크</span><span class="app-name">카카오뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-internet" onclick="prepareTransfer('supertoss://', 'viva.republica.toss')"><span class="bank-name">토스뱅크</span><span class="app-name">토스 (Toss)</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-internet" onclick="prepareTransfer('ukbanksmartbank://', 'com.kbankwith.smartbank')"><span class="bank-name">케이뱅크</span><span class="app-name">케이뱅크</span></button></div>

        <!-- 2. 시중은행 및 국책은행 -->
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('kbbank://', 'com.kbstar.kbbank')"><span class="bank-name">KB국민은행</span><span class="app-name">KB스타뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('hanaez://', 'com.hanabank.ebk.channel.android.hananbank')"><span class="bank-name">하나은행</span><span class="app-name">하나원큐</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('wooribank://', 'com.wooribank.smart.npib')"><span class="bank-name">우리은행</span><span class="app-name">우리WON뱅킹</span></button></div>
        
        <div class="btn-wrap w-2"><button class="bank-btn border-commercial" onclick="prepareTransfer('shinhan-sr://', 'com.shinhan.sbanking')"><span class="bank-name">신한은행</span><span class="app-name">SOL뱅크</span></button></div>
        <div class="btn-wrap w-2"><button class="bank-btn border-commercial" onclick="prepareTransfer('shinhansupersol://', 'com.shinhan.supersol')"><span class="bank-name">신한은행</span><span class="app-name">슈퍼SOL</span></button></div>

        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('nhallone://', 'nh.smart.allone')"><span class="bank-name">NH농협은행</span><span class="app-name">NH올원뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('newnhsmartbanking://', 'nh.smart.banking')"><span class="bank-name">NH농협은행</span><span class="app-name">NH스마트뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('nhcok://', 'nh.smart.cok')"><span class="bank-name">NH농협은행</span><span class="app-name">NH콕뱅크</span></button></div>

        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('ionebank://', 'com.ibk.android.ionebank')"><span class="bank-name">IBK기업은행</span><span class="app-name">i-ONE Bank</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('scbank://', 'com.sc.pub.banking')"><span class="bank-name">제일은행</span><span class="app-name">SC 제일은행</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('citibank://', 'com.citibank.mobile.kr')"><span class="bank-name">씨티은행</span><span class="app-name">씨티모바일</span></button></div>

        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('suhyup://', 'com.suhyup.smartbank')"><span class="bank-name">Sh수협은행</span><span class="app-name">파트너뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('suhyup-sook://', 'com.suhyup.sook')"><span class="bank-name">Sh수협은행</span><span class="app-name">쑥뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('suhyup-hey://', 'com.suhyup.hey')"><span class="bank-name">Sh수협은행</span><span class="app-name">헤이뱅크</span></button></div>

        <div class="btn-wrap w-3"><button class="bank-btn border-commercial" onclick="prepareTransfer('kdbbank://', 'com.kdb.smart')"><span class="bank-name">한국산업은행</span><span class="app-name">스마트KDB</span></button></div>

        <!-- 3. 지방은행 -->
        <div class="btn-wrap w-3"><button class="bank-btn border-regional" onclick="prepareTransfer('mbanking://', 'com.dgb.smartbank')"><span class="bank-name">iM뱅크</span><span class="app-name">iM뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-regional" onclick="prepareTransfer('bsbank://', 'com.bsbank.smartbank')"><span class="bank-name">BNK부산은행</span><span class="app-name">모바일뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-regional" onclick="prepareTransfer('knbank://', 'com.knbank.android.smartbank')"><span class="bank-name">BNK경남은행</span><span class="app-name">모바일뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-regional" onclick="prepareTransfer('kjbank://', 'com.kjbank.smart')"><span class="bank-name">광주은행</span><span class="app-name">광주WA뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-regional" onclick="prepareTransfer('jbpribanksign://', 'com.jbbank.smart')"><span class="bank-name">전북은행</span><span class="app-name">쏙뱅크</span></button></div>

        <div class="btn-wrap w-2"><button class="bank-btn border-regional" onclick="prepareTransfer('jejubank://', 'com.jejubank.smartbank')"><span class="bank-name">제주은행</span><span class="app-name">제주SOL뱅크</span></button></div>
        <div class="btn-wrap w-2"><button class="bank-btn border-regional" onclick="prepareTransfer('jejubank-j://', 'com.jejubank.jbank')"><span class="bank-name">제주은행</span><span class="app-name">J뱅크</span></button></div>

        <!-- 4. 제2금융권 및 상호금융 -->
        <div class="btn-wrap w-3"><button class="bank-btn border-mutual" onclick="prepareTransfer('epost://', 'com.epost.smart')"><span class="bank-name">우체국</span><span class="app-name">우체국 뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-mutual" onclick="prepareTransfer('kfcc://', 'kr.co.kfcc.kfccsmbs')"><span class="bank-name">새마을금고</span><span class="app-name">MG더뱅킹</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-mutual" onclick="prepareTransfer('cuon://', 'kr.co.cu.onbank')"><span class="bank-name">신협</span><span class="app-name">신협ON뱅크</span></button></div>
        <div class="btn-wrap w-3"><button class="bank-btn border-mutual" onclick="prepareTransfer('sbtalk://', 'kr.or.fsb.sbtalktalk')"><span class="bank-name">저축은행중앙회</span><span class="app-name">SB톡톡플러스</span></button></div>
    </div>
</div>

<!-- 팝업 모달창 -->
<div id="copyModal" class="modal-overlay">
    <div class="modal-content">
        <p class="modal-text">
            복권구매 이체계좌 :
            <span class="account-highlight">케이뱅크 100-301-168768 심재희</span>
            로 송금할까요?
        </p>
        
        <!-- 하이퍼링크 기반 앱 호출 앵커 -->
        <a id="confirmLink" href="#" class="confirm-btn" onclick="executeCopy(event)">확인</a>
        
        <!-- 미설치 수동 이동 링크 -->
        <div style="margin-top: 15px; font-size: 0.8rem;">
            <a id="storeLink" href="#" style="color: #666; text-decoration: underline;">앱이 실행되지 않나요? (앱스토어)</a>
        </div>
        
        <button onclick="closeModal()" style="margin-top: 10px; background: none; border: none; color: #999; text-decoration: underline; padding: 5px; cursor: pointer; font-family: 'Paperlogy';">취소</button>
    </div>
</div>

<script>
    const copyData = '케이뱅크 100301168768'; 

    function prepareTransfer(scheme, androidPackageName) {
        var userAgent = navigator.userAgent.toLowerCase();
        var isAndroid = userAgent.indexOf("android") > -1;
        var isIOS = userAgent.indexOf("iphone") > -1 || userAgent.indexOf("ipad") > -1;
        
        var cleanScheme = scheme.replace('://', '');
        
        // 안드로이드는 스킴을 버리고 패키지명만으로 강제 호출 (가장 확실한 방법)
        var appUrl = isAndroid 
            ? "intent://#Intent;package=" + androidPackageName + ";end;" 
            : scheme;
            
        var storeUrl = isAndroid 
            ? "market://details?id=" + androidPackageName 
            : (isIOS ? "https://apps.apple.com/kr/search?term=" + cleanScheme : "#");

        document.getElementById('confirmLink').href = appUrl;
        document.getElementById('storeLink').href = storeUrl;
        
        document.getElementById('copyModal').style.display = 'flex';
    }

    function closeModal() {
        document.getElementById('copyModal').style.display = 'none';
    }

    function executeCopy(event) {
        // 화면 밖에서 텍스트(계좌번호) 클립보드 복사
        var textArea = document.createElement("textarea");
        textArea.value = copyData;
        textArea.style.position = "fixed";
        textArea.style.left = "-9999px";
        document.body.appendChild(textArea);
        textArea.focus();
        textArea.select();
        try {
            document.execCommand('copy');
        } catch (err) {
            console.log("복사 실패");
        }
        document.body.removeChild(textArea);

        // 하이퍼링크가 정상적으로 작동할 시간을 벌어준 뒤 창 닫기
        setTimeout(function() {
            closeModal();
        }, 800);
    }
</script>

</body>
</html>
