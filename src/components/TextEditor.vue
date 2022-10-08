<template>
<div class='root'>
	<!--Панель инструменов првки текста-->
	<fieldset>
		<button class="fontStyle" @click="bold">Жирный</button>
		<button class="fontStyle" @click="italic">Курсив</button>
		<button class="fontStyle" @click="underline">Подчеркивание</button>
		<!--Выбор шрифта-->
		<select v-model="currentFont" @change="selectFont"> 
			<option v-for="font in fonts" :key="font">{{font}}</option>
		</select>
		<!--Выбор размера шрифта-->
		<select v-model="currentFontSize" @change="selectFontSize">
			<option v-for="size in aviableSizes" :key="size">{{size}}</option>
		</select>
	</fieldset>
	<!--поле ввода текста-->
	<div id='editor' contenteditable="true" 
	@focus="$event.target.value" 
	ref="textArea">
		{{text}}
	</div>
</div>
</template>

<script>
	export default{
		name: 'textEditor',
		data() {
			return {
				text: 'Введите ответ', // вводимый текст
				focusedText: '', // выделенный текст
				fonts: ["Georgia", "Times New Roman", "Arial Black", "Comic Sans MS",
				"Courier New", "Tahoma"], // доступные шрифты
				currentFont: "Times New Roman", // текущий шрифт
				currentFontSize: 3, // текущий размер шрифта
				aviableSizes: this.getRangeFontSizes(1,7) // доступные размеры шрифта
			} 
		},

		methods:{
			// Выделение жирным
			bold(){
				this.$refs.textArea.focus();
				document.execCommand('bold', false, null);
			},
			// выделение курсивом
			italic(){
				this.$refs.textArea.focus();
				document.execCommand('italic', false, null);
			},
			// подчеркивание
			underline(){
				this.$refs.textArea.focus();
				document.execCommand('underline', false, null);				
			},
			// выбор шрифта
			selectFont(){
				this.$refs.textArea.focus();
				document.execCommand('fontName', false, this.currentFont);
			},
			// выбор размера шрифта
			selectFontSize(){
				this.$refs.textArea.focus();
				document.execCommand('fontSize', true, this.currentFontSize);
			},
			// доступные размеры шрифта
			getRangeFontSizes(start, end){
				var sizes = [];
				for(var i=start;i<=end;i++){
					sizes.push(i);
				}
				return sizes;
			}

		}
	}

</script>
