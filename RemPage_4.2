// ==UserScript==
// @name        RemPage
// @namespace        http://tampermonkey.net/
// @version        4.2
// @description        ブログページ拡大表示をブログ単位で記録・固定(zoom使用)
// @author        Ameba Blog User
// @match        https://ameblo.jp/*
// @exclude        https://ameblo.jp/*/image*
// @icon        https://www.google.com/s2/favicons?sz=64&domain=ameblo.jp
// @run-at        document-start
// @noframes
// @grant        none
// @updateURL        https://github.com/personwritep/RemPage/raw/main/RemPage.user.js
// @downloadURL        https://github.com/personwritep/RemPage/raw/main/RemPage.user.js
// ==/UserScript==



let ua=0;
let agent=window.navigator.userAgent.toLowerCase();
if(agent.indexOf('firefox') > -1){ ua=1; } // Firefoxの場合のフラッグ



let remember_data={}; // ブログ登録データ
let remember_id=[];
let remember_zoom=[];
let z_button;
let user_id;
let zoom_value;
let zoom_auto=0;
let edit_mode=0;


reg_set();

function reg_set(){
    let read_json=localStorage.getItem('remember_zoom'); // ローカルストレージ 保存名
    remember_data=JSON.parse(read_json);
    if(remember_data==null){
        remember_data=[['user', 'zoom']]; } // ブログ記事データ

    remember_id=[]; // 配列をリセット
    remember_zoom=[]; // 配列をリセット
    for(let k=0; k<remember_data.length; k++){
        remember_id[k]=remember_data[k][0];
        remember_zoom[k]=remember_data[k][1]; }}



let retry=0;
let interval=setInterval(wait_target, 1);
function wait_target(){
    retry++;
    if(retry>100){ // リトライ制限 100回 0.1secまで
        clearInterval(interval); }
    let target=document.body; // 監視 target
    if(target){
        clearInterval(interval);
        zoom_startup(); }}



function zoom_startup(){
    do_zoom();

    setTimeout(()=>{
        center(); }, 100);

    let target0=document.querySelector('head'); // 監視 target
    let monitor0=new MutationObserver(do_zoom);
    monitor0.observe(target0, { childList: true }); // 監視開始

    let target1=document.querySelector('#announcer'); // 監視 target
    if(target1){
        let monitor1=new MutationObserver(path_change);
        monitor1.observe(target1, { childList: true }); } // 監視開始

} // zoom_startup()



function do_zoom(){
    zoom_reset();
    center();
    backup_set(); }



function zoom_reset(){
    user_id=document.location.pathname.split("/")[1]; // ユーザーIDを取得

    if(remember_id.indexOf(user_id)!=-1){
        zoom_value=remember_zoom[remember_id.indexOf(user_id)];
        if(zoom_value==1){
            zoom_auto=3; } // 登録有 100% zoom を適用
        else { zoom_auto=2; }} // 登録有 manual zoom を適用
    else{
        let entryBody=document.querySelector('#entryBody');
        if(entryBody){
            if(getComputedStyle(entryBody, null).fontSize=='14px'){ // 未登録14px型
                zoom_auto=1; // 未登録 auto zoom を適用
                zoom_value=1.14; }
            else{
                zoom_auto=0; // 未登録 zoom 無し
                zoom_value=1; }}
        else{
            zoom_auto=0; // 未登録 zoom 無し
            zoom_value=1; }} // entryBodyが取得出来ない場合

    rp_zoom(zoom_value); // 拡大実行

} // zoom_reset() zoom値の選択と拡大実行



function rp_zoom(val){ // ページ拡大コードを生成
    let style;

    if(val!=1){
        style=
            '<style id=rpzoom>'+
            'body { zoom: '+ val +' } '+
            '#ambHeader, footer, .ReactModalPortal { zoom: '+ 1/val +' } '+
            '._sMG87wzO, ._5TpaM9FS { display: none } ';
        if(ua==1){
            style+=
                'html { font-size: '+ (htm_font())*val +'%; }'; }}
    else{
        style=
            '<style id=rpzoom>'+
            '._sMG87wzO, ._5TpaM9FS { display: none } '; }

    style+=
        '#ambHeader img[alt="Ameba"] { filter: contrast(6) hue-rotate(90deg); ';

    if(zoom_auto==0){ // 未登録 zoom 無し
        style+=
            'box-shadow: none; padding-left: 0 }</style>'; }
    else if(zoom_auto==1){ // 未登録 auto zoom
        style+=
            'box-shadow: -10px 0 0 #e98200; padding-left: 5px }</style>'; }
    else if(zoom_auto==2){ // 登録有 manual zoom
        style+=
            'box-shadow: -10px 0 0 #7aff00; padding-left: 5px }</style>'; }
    else if(zoom_auto==3){ // 登録有 100% zoom
        style+=
            'box-shadow: -10px 0 0 #9c27b0; padding-left: 5px }</style>'; }

    if(!document.querySelector('#rpzoom')){
        document.documentElement.insertAdjacentHTML('beforeend', style); }


    function htm_font(){ // htmlのfont-size指定を取得
        let out;
        let htm=document.documentElement;
        if(htm){
            let f_size=window.getComputedStyle(htm).getPropertyValue('font-size');
            if(f_size){
                let f_per=parseInt(f_size.replace(/[^0-9^\.]/g,""), 10) /16;
                if(f_per){
                    out=Number.parseFloat(f_per).toFixed(2)*100; }}} // %値に変換

        if(50<out<200){
            return out; } // htmlにfont-size指定があれば取得
        else{
            return 100; } // htmlにfont-size指定が無い場合は 100

    } // htm_font()

} // rp_zoom()



function center(){ // 記事本文を中央に配置
    let ht=document.documentElement.scrollTop;
    let main_a=document.querySelector('#main');
    if(main_a){
        let cr_left=main_a.getBoundingClientRect().left;
        let cr_width=main_a.getBoundingClientRect().width;
        let center_p=cr_left + cr_width/2;
        let v_center=center_p*zoom_value;
        let window_w=document.documentElement.clientWidth;
        let scrooll_step=v_center - window_w/2
        if(ht<10){ // 縦スクロール後は動作しない
            if(scrooll_step>10 || scrooll_step<-10){
                scrollBy(scrooll_step, 0 ); }}}}



function backup_set(){
    z_button=document.querySelector('#ambHeader img[alt="Ameba"]');
    if(z_button){
        z_button.onclick=function(event){ // Amebaアイコンのクリック
            event.preventDefault(); // クリックしてもホームに飛ばさない
            backup(); }}}



function backup(){
    edit_mode=1;
    disp_panel();

    let z_panel=document.querySelector('#z_panel');
    if(z_panel){

        let z_close=z_panel.querySelector('#z_close');
        z_close.onclick=function(){
            edit_mode=0;
            zoom_reset();
            z_panel.remove(); }


        let z_num=z_panel.querySelector('#z_num');
        z_num.value=Math.round(zoom_value*100);
        document.onwheel=function(event){ // マスウホイールで設定
            event.stopPropagation();
            event.stopImmediatePropagation();
            if(event.deltaY<0 && edit_mode==1){
                z_num.stepUp(); }
            else if(event.deltaY>0 && edit_mode==1){
                z_num.stepDown(); }
            if(edit_mode==1){
                remove_style();
                rp_zoom(z_num.value/100); }}


        z_num.onchange=function(event){
            event.stopPropagation();
            event.stopImmediatePropagation();
            if(edit_mode==1){
                if(z_num.value<80){
                    z_num.value=80; }
                else if(z_num.value>200){
                    z_num.value=200; }
                remove_style();
                rp_zoom(z_num.value/100); }}


        let z_set=z_panel.querySelector('#z_set');
        z_set.onclick=function(){
            let zoom_set=z_num.value/100; // 登録するzoom倍率

            if(remember_id.indexOf(user_id)==-1){ // 未登録のIDの場合
                remember_data.push([user_id, zoom_set]); // 等倍も登録する
                let write_json=JSON.stringify(remember_data);
                localStorage.setItem('remember_zoom', write_json); }
            else if(remember_id.indexOf(user_id)!=-1){ // 既登録のIDの場合
                remember_data.splice(remember_id.indexOf(user_id), 1); // 一旦は登録削除
                remember_data.push([user_id, zoom_set]); // 登録値を更新して追加
                let write_json=JSON.stringify(remember_data);
                localStorage.setItem('remember_zoom', write_json); }

            reg_set();
            edit_mode=0;
            remove_style();
            do_zoom();
            z_panel.remove(); }


        let z_reset=z_panel.querySelector('#z_reset');
        z_reset.onclick=function(){
            if(remember_id.indexOf(user_id)==-1){ ; } // 未登録のIDの場合
            else if(remember_id.indexOf(user_id)!=-1){ // 既登録のIDの場合
                remember_data.splice(remember_id.indexOf(user_id), 1); // Resetは登録削除
                let write_json=JSON.stringify(remember_data);
                localStorage.setItem('remember_zoom', write_json); }

            reg_set();
            edit_mode=0;
            remove_style();
            do_zoom();
            z_panel.remove(); }


        let z_exp=z_panel.querySelector('#z_exp');
        z_exp.onclick=function(){
            let write_json=JSON.stringify(remember_data);
            let blob=new Blob([write_json], {type: 'application/json'});
            try{
                let a_elem=document.createElement('a');
                a_elem.href=URL.createObjectURL(blob);
                document.body.appendChild(a_elem);
                a_elem.download='remember_zoom.json'; // 保存ファイル名
                a_elem.click();
                URL.revokeObjectURL(a_elem.href);
                alert("✅  ファイルを保存しました\n"+
                      "　　ダウンロードフォルダーを確認してください"); }
            catch(e){
                alert("❌ ファイル保存時にエラーが発生しました\n"+
                      "　　ダウンロードフォルダーを確認してください"); }}


        let z_imp=z_panel.querySelector('#z_imp');
        let z_file=z_panel.querySelector('#z_file');
        z_imp.onclick=function(){
            z_file.click(); }

        z_file.addEventListener("change" , function(){
            if(!(z_file.value)) return; // ファイルが選択されない場合
            let file_list=z_file.files;
            if(!file_list) return; // ファイルリストが選択されない場合
            let file=file_list[0];
            if(!file) return; // ファイルが無い場合

            let file_reader=new FileReader();
            file_reader.readAsText(file);
            file_reader.onload=function(){
                if(file_reader.result.slice(0, 15)=='[["user","zoom"'){ // ファイルデータの確認
                    remember_data=JSON.parse(file_reader.result); // 読出してストレージを上書きする
                    let write_json=JSON.stringify(remember_data);
                    localStorage.setItem('remember_zoom', write_json); // ローカルストレージ 保存名
                    reg_set();
                    zoom_reset(); // 画面の拡大表示をリセット
                    alert("✅　拡大率の登録データを読込みました\n"+
                          "　　　読込んだファイル名:　" + file.name); }
                else{
                    alert("❌　Remember My Page の Exportファイルではありません\n"+
                          "　　　Importファイルは 「remember_zoom ... 」の名前です"); }}});


        let dp=window.devicePixelRatio;
        let browser_mag=Math.round(dp*100);
        let z_mag=z_panel.querySelector('#z_mag');
        if(browser_mag!=100){
            z_mag.innerHTML='Basic ' + browser_mag + '%';

            z_panel.style.zIndex='2';
            setTimeout(()=>{
                z_mag.style.opacity='0';
            }, 3000);
            setTimeout(()=>{
                z_mag.style.display='none';
                z_panel.style.zIndex='0';
            }, 6000); }
        else{
            z_mag.style.display='none'; }

    } // if(z_panel)
} // backup()



function remove_style(){
    if(document.querySelector('#rpzoom')){
        document.querySelector('#rpzoom').remove(); }}



function disp_panel(){
    let z_div=
        '<div id="z_panel">'+
        '<input id="z_close" type="submit" value="×">'+
        '<input id="z_num" type="number" step="5" min="80" max="200">'+
        '<input id="z_set" type="submit" value="Set">'+
        '<input id="z_reset" type="submit" value="Reset">'+
        '<input id="z_exp" type="submit" value="Export">'+
        '<input id="z_imp" type="submit" value="Import">'+
        '<input id="z_file" type="file">'+
        '<span id="z_mag"></span>'+
        '<style>'+
        'html { overflow: hidden; } '+
        '#z_panel { position: absolute; top: 7px; left: 0; z-index: 0; '+
        'color: #333; background: #fff; padding: 5px 0 5px 15px; width: 400px; } '+
        '#z_panel input[type="number"]::-webkit-inner-spin-button { '+
        '-webkit-appearance: none; margin: 0; } '+
        '#z_panel input[type="number"] { -moz-appearance:textfield; } '+
        '#z_panel > * { font: normal 15px Arial; padding: 2px; height: 24px; } '+
        '#z_close { font-weight: bold; width: 14px; padding: 2px 0; margin-right: 15px; } '+
        '#z_num { width: 36px; padding: 1.5px 0 0 8px; height: 18.8px; '+
        'box-sizing: content-box; } '+
        '#z_set { margin-left: 4px; } '+
        '#z_reset { margin-left: 4px; } '+
        '#z_exp { margin: 0 4px 0 15px; } '+
        '#z_imp { margin-right: 15px; } '+
        '#z_file { display: none; } '+
        '#z_mag { color: #fff; background: #0288d1; padding: 3px 4px; '+
        'border: thin solid #888; border-radius: 3px; transition: 2s; } '+
        '</style></div>';

    if(!document.querySelector('#z_panel')){
        document.querySelector('#ambHeader div:first-child')
            .insertAdjacentHTML('beforeend', z_div); }

} // disp_panel()



function path_change(){ // zoomの設定中にページ変更をした場合の error抑止
    if(edit_mode==1){
        edit_mode=0;
        let z_panel=document.querySelector('#z_panel');
        if(z_panel){
            z_panel.remove(); }}

} // path_change()
