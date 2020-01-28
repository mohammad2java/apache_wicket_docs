
##Apache Wicket UserGuide
-----------------------
	1) Installation
	2) Basic concept
	3) Form and validation
	4) Internationalization and externalization
	5) Pop-up or ModelWindow
	6) DataList or showing data in tabular form
	7) Ajax for communication
	8) Integration
	9) Securing application


##Installation ( how to generated wicket application using maven)
----------------------------------------------------------------------

	1) go to https://wicket.apache.org/start/quickstart.html
	2) fill group and artifact id and using generated mvn command.
	3) Import generated project into eclipse.
	 				or 
	 using eclipse create maven application and select architype as 'wicket-archetype-quickstart'
 



##Basic Concept
------------------
	its event based framework like swing but swing is for  desktop application
	There are a lots of competitors framework like-JSF,VAADIN etc...
	
	in MVC framework we do request and response.
	----------------------------------------------
	Application =front-end+back-end  
	front-end=UI Designer(html,css and framework) + UI developers(javascript,jquery and framework) 
	back-end = Controller+Service+DAO+DB.
	
	in Event Based Application we dont required UI developers
	----------------------------------------------------------- 
	Application = front-end+back-end
	front-end= UI Designer only
	back-end = Wicket+Service+DAO+DB
	
	as per above formula if you compare to MVC application patterns - wicket is working as "UI developers+Controllers"


	Must To Have Notes
	-------------------
	for every elements of html , wicket provides respective elements that wicket elements is known as Components
	and html element bind to respective wicket components using wicket-id.
	there are two version of components( regular and ajaxVersion)
	Imodel is used to provide dynamic data to the html elements
	
	every page in wicket application having atleast two PpageName.html and PageName.java)
	both files must be in same class-path.
	
	
1) Base Components list
-------------------------------
	Output:
	------------------------------------
	wicket.markup.html.basic.Label
	wicket.markup.html.basic.MultiLineLabel
	alternative markup (XML)
	
	Layout and grouping:
	-------------------------
	wicket.markup.html.panel.Panel
	wicket.markup.html.border.Border
	wicket.markup.html.include.Include
	wicket.markup.html.tabs.TabbedPanel (wicket-extensions)
	wicket.markup.html.panel.Fragment
	
	Links (for more examples, see Link-o-matic):
	---------------------------------------------
	wicket.markup.html.link.Link
	wicket.markup.html.link.ExternalLink
	wicket.markup.html.link.BookmarkablePageLink
	
	Forms (for more examples, see FormInput):
	---------------------------------------------
	wicket.markup.html.form.Form
	wicket.markup.html.form.Button
	wicket.markup.html.form.SubmitLink
	wicket.markup.html.form.TextField
	wicket.markup.html.form.TextArea
	wicket.markup.html.form.CheckBox
	wicket.markup.html.form.CheckGroup 
	wicket.markup.html.form.Check 
	wicket.markup.html.form.CheckGroupSelector
	wicket.markup.html.form.CheckGroup 
	and wicket.markup.html.form.CheckGroupSelector
	wicket.markup.html.form.CheckBoxMultipleChoice
	wicket.markup.html.form.CheckBoxSelector
	wicket.markup.html.form.DropDownChoice
	wicket.markup.html.form.ListChoice
	wicket.markup.html.form.RadioChoice
	wicket.markup.html.form.RadioGroup 
	wicket.markup.html.form.Radio
	wicket.markup.html.form.ListMultipleChoice
	wicket.extensions.markup.html.form.select.Select
	wicket.extensions.markup.html.palette.Palette
	
	
##Form and validation
----------------------
1) A sample example of Login page
------------------------------
	
	1) create html page as designer..
	
	LoginPage.html
	--------------
	<html xmlns:wicket="http://wicket.apache.org">
	<h1>User Login</h1>
	<div wicket:id="feedback"></div>
	<body>
	<form wicket:id="loginform">
	<span wicket:id="label1"></span><input type="text" wicket:id="username"/>
	<span wicket:id="label2"></span><input type="password" wicket:id="password"/>
	<input type="submit"/>
	</form>
	</body>
	</html>
	
	2) create WebPage respective to HtmlPage mapped all wicket:id components in java.
	
	LoginPage.java
	-------------------
	public class LoginPage extends WebPage {
		private static final long serialVersionUID = 1L;
		private String name;
		private String pass;

		public LoginPage() {
			FeedbackPanel feedbackPanel = new FeedbackPanel("feedback");
			add(feedbackPanel);
			Form<?> form = new Form<Object>("loginform") {
				private static final long serialVersionUID = 1L;
				@Override
				protected void onSubmit() {
				 info("Entered UserName is: "+getName());
				 info("Entered UserPass is: "+getPass());
				}
			};
			
			form.add(new Label("label1","EnterUsername"));
			form.add(new TextField<String>("username",new PropertyModel<String>(this,"name")).setRequired(true));
			form.add(new Label("label2","EnterPassword"));
			form.add(new PasswordTextField("password" ,new PropertyModel<String>(this,"pass")).setRequired(true));
			add(form);
		}
	
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public String getPass() {
			return pass;
		}
		public void setPass(String pass) {
			this.pass = pass;
		}}
	
	
		Notes about above code.. 
		1) info() method used FeedbackPanel to display message.Feedbackpanel always used to display message.
		2) PropertyModel used to mapped html elements data to object fields to process further at server side.
		3) Label --> for heading/labeling...
		4) TextField--> for input type="text"
		5) PasswordTextField--> for input type="password"
		
			
	
