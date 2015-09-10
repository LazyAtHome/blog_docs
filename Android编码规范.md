#Android Coding Style

##preview

  Android的源代码主要分三大类，.java文件（src文件夹中）和资源文件（res文件夹中）以及注释；编码规范主要说明了不同类型的资源文件的命名方式，以及.java源文件的编写规范。

##.java

###1.包命名
   命名规则：一个唯一包名的前缀总是全部小写的ASCII 字母并且是一个顶级域名，通常是com，edu，gov，mil，net，org。包名的后续部分根据不同机构各自内部的命名规范而不尽相同。这类命名规范可能以特定目录名的组成来区分部门 (department) ，项目(project)，机器(machine)，或注册名(login names)。
例如： com.hymobile.nloc.activities

规约：包命名必须以com.hymobile开始，后面跟有项目名称（或者缩写）,再后面为模块名或层级名称。
如：com.hymobile.项目缩写.模块名  com.hymobile.nloc.bookmark
如：com.hymobile.项目缩写.层级名  com.hymobile.nloc.activities

###2.类和接口 命名
   命名规则：类名是个一名词，采用大小写混合的方式，每个单词的首字母大写。尽量使你的类名简洁而富于描述。使用完整单词，避免缩写词(除非该缩写词被更广泛使用，像 URL，HTML)  
接口一般要使用able、ible、er 等后缀
例如： class Raster;  class ImageSprite;

规约：类名必须使用驼峰规则，即首字母必须大写，如果为词组，则每个单词的首字母也必须要大写，类名必须使用名词，或名词词组。要求类名简单，不允许出现无意义的单词（如 class XXXActivity）。
如：class BookMarkAdd  正确
如：class AddBookReadPlanActivity 
###3.方法的命名
 命名规则：方法名是一个动词，采用大小写混合的方式，第一个单词的首字母小写，其后单词的首字母大写。
例如： public void run(); public String getBookName();

####类中常用方法的命名：
1.类的获取方法（一般具有返回值）一般要求在被访问的字段名前加上get，如
getFirstName()，getLastName()。一般来说，get前缀方法返回的是单个值，find前缀的方法返回的是列表值。
2.类的设置方法（一般返回类型为void）：被访问字段名的前面加上前缀 set，如
setFirstName(),setLastName().
3.类的布尔型的判断方法一般要求方法名使用单词 is或has 做前缀，如isPersistent()，isString()。或者使用具有逻辑意义的单词，例如equal 或equals。
4.类的普通方法一般采用完整的英文描述说明成员方法功能，第一个单词尽可能采用动词，首字母小写，如openFile（），addCount（）。
5.构造方法应该用递增的方式写。（参数多的写在后面）。
6.toString()方法：一般情况下，每个类都应该定义toString()
###4.变量命名
命名规则：第一个单词的首字母小写，其后单词的首字母大写。变量名不应以下划线或美元符号开头，尽管这在语法上是允许的。变量名应简短且富于描述。变量名的选用应该易于记忆，即，能够指出其用途。尽量避免单个字符的变量名，除非是一次性的临时变量。临时变量通常被取名为 i，j，k，m 和 n，它们一般用于整型；c，d，e，它们一般用于字符型。
例如：String bookName; 

规约：变量命名也必须使用驼峰规则，但是首字母必须小写，变量名尽可能的使用名词或名词词组。同样要求简单易懂，不允许出现无意义的单词。
如：String bookName;
###5.成员变量的命名
同变量命名，但不要在私有变量前添加m字样！封装数据的实体类一般不需要
###6.常量的命名
命名规则：类常量的声明，应该全部大写，单词间用下划线隔开。
例如：static final int MIN_WIDTH = 4; 
例如：static final int MAX_WIDTH = 999; 
例如：static final int GET_THE_CPU = 1

##资源文件

###1.layout的命名
规约：layout xml 的命名必须以 全部单词小写，单词间以下划线分割，并且使用名词或名词词组，即使用 模块名_功能名称 来命名。
如：knowledge_gained_main.xml
###2.id的命名
规约：layout 中所使用的id必须以全部单词小写，单词间以下划线分割，并且使用名词或名词词组，并且要求能够通过id直接理解当前组件要实现的功能。
如：某TextView @+id/text_book_name 
如：某EditText @+id/edit_book_name
###3.资源文件的命名
规约：layout中所使用的所有资源（如drawable,style等）命名必须以全部单词小写，单词间以下划线分割，并且尽可能的使用名词或名词组，即使用 模块名_用途 来命名。如果为公共资源，如分割线等，则直接用用途来命名
如：menu_icon_navigate.png 
如：某分割线：line.png  或 separator.png 

##注释
###1.文件注释
所有的源文件都应该在开头有一个注释，其中列出类名、版本信息、日期和版权声明。
如下：
  /*
   * 文件名 
   * 包含类名列表
   * 版本信息，版本号
   * 创建日期。
   * 版权声明
   */
###2.类注释
每一个类都要包含如下格式的注释，以说明当前类的功能等。

/**
 * 类名
 * @author 作者 <br/>
 *	实现的主要功能。
 *	创建日期
*	修改者，修改日期，修改内容。
*/
###3.方法注释
每一个方法都要包含 如下格式的注释 包括当前方法的用途，当前方法参数的含义，当前方法返回值的内容和抛出异常的列表。

/**
	 * 
	 * 方法的一句话概述
	 * <p>方法详述（简单方法可不必详述）</p>
	 * @param s 说明参数含义
	 * @return 说明返回值含义
	 * @throws IOException 说明发生此异常的条件
	 * @throws NullPointerException 说明发生此异常的条件
	 */
###4.类成员变量和常量注释
成员变量和常量需要使用java doc形式的注释，以说明当前变量或常量的含义
/**
* XXXX含义
  */
###5.行间注释
方法内部的注释 如果需要多行 使用/*…… */形式，如果为单行是用//……形式的注释。不要再方法内部使用 java doc 形式的注释“/**……**/”，简单的区分方法是，java doc形式的注释在 eclipse中为蓝色，普通注释为绿色。
###6.xml注释
规约：如果当前layout 或资源需要被多处调用，或为公共使用的layout（若list_item），则需要在xml写明注释。要求注释清晰易懂。


- 