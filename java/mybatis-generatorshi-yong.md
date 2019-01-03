* 导入项目
* 配置文件
  * generatorConfig.xml

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE generatorConfiguration
    PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
    "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

  <generatorConfiguration>


    <context id="DB2Tables" targetRuntime="MyBatis3">
    
      /*去掉注释*/
      <commentGenerator>
      	<property name="suppressDate" value="true"/>
      	<property name="suppressAllComments" value="true" />
    	</commentGenerator>
  
      <jdbcConnection driverClass="com.mysql.jdbc.Driver"
          connectionURL="jdbc:mysql://127.0.0.1:3306/crm"
          userId="root"
          password="123456">
      </jdbcConnection>

      <javaTypeResolver >
        <property name="forceBigDecimals" value="false" />
      </javaTypeResolver>

      <javaModelGenerator targetPackage="com.crm.pojo" targetProject=".\src">
        <property name="enableSubPackages" value="true" />
        <property name="trimStrings" value="true" />
      </javaModelGenerator>

      <sqlMapGenerator targetPackage="com.crm.mapper"  targetProject=".\src">
        <property name="enableSubPackages" value="true" />
      </sqlMapGenerator>

      <javaClientGenerator type="XMLMAPPER" targetPackage="com.crm.mapper"  targetProject=".\src">
        <property name="enableSubPackages" value="true" />
      </javaClientGenerator>
    
  	<table schema="" tableName="base_dict">
  		<property  name="useActualColumnNames"  value="false" />  
  	</table>
  	<table schema="" tableName="cst_linkman">
  		<property  name="useActualColumnNames"  value="false" />  
  	</table>
  	<table schema="" tableName="customer">
  		<property  name="useActualColumnNames"  value="false" />  
  	</table>
  	<table schema="" tableName="sys_user">
  		<property  name="useActualColumnNames"  value="false" />  
  	</table>
    </context>
  </generatorConfiguration>


  ```

  * 



