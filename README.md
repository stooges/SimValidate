# SimValidate


一、说明
 1. 功能
 
 （1）校验一组html控件内容的合法性，该组控件可以属于一个form也可以在\<div\>或其他html元素中；

 （2）支持自动校验与手动校验；
 
 （3）自动校验支持动态事件绑定；
 
 （4）支持手机端控件；
 
 （5）支持对控件组校验（例如，一组checkbox或ratiobox）;
 
 （6）支持用户自定义校验器。
 
 2. html属性
 
 （1）test-id：被校验控件或控件组的校验id；

 （2）message-for：校验信息隶属于哪个被校验控件，基值为被校验控件的test-id；
 
 （3）test-type：校验信息的类型，与message-for同时使用；
 
 （4）test-point：待校验控件组中的校验点，即组中的单个控件；
 
 （5）required, groupRequired, number, max, min, minlength, email, idcard, mobile, equalTo，以及自定义校验器的名字，用于标识待校验控件的校验类型；
 
 3. 使用方法
	
 （1）html代码

		<div id="inputs_elements">
 			<div>
 				<input type="text" test-id="element1" required/>
 				<span message-for="element1">不能为空</span>
 			</div>
 			<div>
 				<input type="text" test-id="element2" required number max="100" min="50"/>  
 				<!--非空的大于等50小于等于100的数字-->
 				<span message-for="element2" test-type="required">不能为空</span>
 				<span message-for="element2" test-type="number">必须输入数字</span>
 				<span message-for="element2" test-type="max">最大值为100</span>
 				<span message-for="element2" test-type="min">最小值为50</span>
 			</div>
 			<div>
 				<div test-id="group1" groupRequired>  <!--一组checkbox必须选择至少一个-->
 					<input type="checkbox" test-point>
 					<input type="checkbox" test-point>
 					<input type="checkbox" test-point>
 				</div>
 				<span message-for="group1" test-type="groupRequired">必须选择至少一个</span>
 			</div>
 			<div><!-- 一组值不能重复 -->
  		        <input type="text" test-id="value1" distinct="value">
  		        <span message-for="value1" test-type="distinct">数值重复</span>
  		        <input type="text" test-id="value2" distinct="value">
  		        <span message-for="value2" test-type="distinct">数值重复</span>
  		        <input type="text" test-id="value3" distinct="value">
  		        <span message-for="value3" test-type="distinct">数值重复</span>
  		    </div>
 		</div>

 （2）JS代码

		a.创建校验对象
			var validate1 = $("#inputs_elements").SimValidate({  //**** 该函数参数可选
				autoTest:true,	//是否自动校验(onblur事件)，默认为true
				shortTest:true,	//是否短路校验，默认为true
				messageStyle:"color:red;padding-left:3px;padding-right:3px",//显示消息的样式，些处为默认值
				});
		b. 自定义校验器
			注意：校验器名必须为合法js标识符（不能包括中划线）
			validate1.extend({
				validator_name : function(value, param, $element, obj){ 
					//value: 待校验对象的输入值;
					//param: 校验类型的取值（如 max="20" 中的值 20）;
					//$element: 待校验对象的Jquery对象;
					//obj: 当前的SimValidate对象。
					...
					return true; // or false
				}
			})
		c. 手动校验
			var result = validate1.validate(); 当所有元素检验都通过时，返回true，否则返回false
