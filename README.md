/*
How to use:
1)Create new file.
2)
*/

function kana2upper(string) {

	var arrayedString = string.split('');
	var value = '';

	var triTable = {
	};
	var biTable = {  
	};
/**
 * 半角カタカナを全角カタカナに変換
 * 
 * @param {String} str 変換したい文字列
 */
	var uniTable = {
        'ｶﾞ': 'ガ', 'ｷﾞ': 'ギ', 'ｸﾞ': 'グ', 'ｹﾞ': 'ゲ', 'ｺﾞ': 'ゴ',
        'ｻﾞ': 'ザ', 'ｼﾞ': 'ジ', 'ｽﾞ': 'ズ', 'ｾﾞ': 'ゼ', 'ｿﾞ': 'ゾ',
        'ﾀﾞ': 'ダ', 'ﾁﾞ': 'ヂ', 'ﾂﾞ': 'ヅ', 'ﾃﾞ': 'デ', 'ﾄﾞ': 'ド',
        'ﾊﾞ': 'バ', 'ﾋﾞ': 'ビ', 'ﾌﾞ': 'ブ', 'ﾍﾞ': 'ベ', 'ﾎﾞ': 'ボ',
        'ﾊﾟ': 'パ', 'ﾋﾟ': 'ピ', 'ﾌﾟ': 'プ', 'ﾍﾟ': 'ペ', 'ﾎﾟ': 'ポ',
        'ｳﾞ': 'ヴ', 'ﾜﾞ': 'ヷ', 'ｦﾞ': 'ヺ',
        'ｱ': 'ア', 'ｲ': 'イ', 'ｳ': 'ウ', 'ｴ': 'エ', 'ｵ': 'オ',
        'ｶ': 'カ', 'ｷ': 'キ', 'ｸ': 'ク', 'ｹ': 'ケ', 'ｺ': 'コ',
        'ｻ': 'サ', 'ｼ': 'シ', 'ｽ': 'ス', 'ｾ': 'セ', 'ｿ': 'ソ',
        'ﾀ': 'タ', 'ﾁ': 'チ', 'ﾂ': 'ツ', 'ﾃ': 'テ', 'ﾄ': 'ト',
        'ﾅ': 'ナ', 'ﾆ': 'ニ', 'ﾇ': 'ヌ', 'ﾈ': 'ネ', 'ﾉ': 'ノ',
        'ﾊ': 'ハ', 'ﾋ': 'ヒ', 'ﾌ': 'フ', 'ﾍ': 'ヘ', 'ﾎ': 'ホ',
        'ﾏ': 'マ', 'ﾐ': 'ミ', 'ﾑ': 'ム', 'ﾒ': 'メ', 'ﾓ': 'モ',
        'ﾔ': 'ヤ', 'ﾕ': 'ユ', 'ﾖ': 'ヨ',
        'ﾗ': 'ラ', 'ﾘ': 'リ', 'ﾙ': 'ル', 'ﾚ': 'レ', 'ﾛ': 'ロ',
        'ﾜ': 'ワ', 'ｦ': 'ヲ', 'ﾝ': 'ン',
        'ｧ': 'ァ', 'ｨ': 'ィ', 'ｩ': 'ゥ', 'ｪ': 'ェ', 'ｫ': 'ォ',
        'ｯ': 'ッ', 'ｬ': 'ャ', 'ｭ': 'ュ', 'ｮ': 'ョ',
        '｡': '。', '､': '、', 'ｰ': 'ー', '｢': '「', '｣': '」', '･': '・'
	};

	if(triTable[string] !== undefined){
        return triTable[string];
	} else if(biTable[string] !== undefined) {
        return biTable[string];
	}

    var biCheck = new Object();
    for (var k in biTable){
        var tmp = k.split('');
        biCheck[tmp[0]] = true;
    }

    var triCheck = new Object();
    for (var tk in triTable){
        var tmp = tk.split('');
        triCheck[tmp[0] + tmp[1]] = true;
        biCheck[tmp[0]] = true; 
    }
    

	var buf = '';
	for(var i = 0; i < arrayedString.length ; i++){
        var str = arrayedString[i];
        buf += str;
        if(buf.length == 3){
            if(triTable[buf] !== undefined){
                value += triTable[buf];
            } else {
                tmp = buf.split('');
                value += biTable[tmp[0] + tmp[1]];
                value += uniTable[tmp[2]] === undefined ? tmp[2] : uniTable[tmp[2]];
                
            }

        } else if(buf.length == 2) {
            if(triCheck[buf] !== undefined) { 
            } else if(biTable[buf] !== undefined) {
                    value += biTable[buf];
                    buf = '';
                } else {
                    tmp = buf.split('');
                    value += uniTable[tmp[0]]; 
                    value += uniTable[tmp[1]] === undefined ? tmp[1] : uniTable[tmp[1]]; 
                    buf = '';
                } 
        } else if(biCheck[buf] !== undefined){
        } else { 
                value += uniTable[str] === undefined ? str : uniTable[str];
                buf = '';
        }


        }

        value += buf !== '' ? uniTable[buf] : '';

    value = value.replace(/([aiueo])ー/gi,'$1');
	return value;
}
