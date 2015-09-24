# SimValidate
前端输入检验
 
一、说明
 1. 功能
 （1）校验一组html控件内容的合法性，该组控件可以属于一个form也可以在<div>或其他html元素中；
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
 （5）required, groupRequired, number, max, min, minlength, email, idcard, mobile，以及自定义校验器的名字，用于标识待校验控件的校验类型；
 3. 使用方法
	参见 SimValidate.js
