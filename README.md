每个人都有自己代码生成器<br />
这个是C# 的用于生成代码的T4模板，只有实体类，数据访问层，业务逻辑层，生成的代码是基于DBHelper.cs 文件，当然，这里提供的DBHelper也是很简单的版本。
<h1>使用说明</h1>
<P>1、打开 config.ttinclude 文件，将myNameSpace 的值改为项目的名字空间；将myConnectionString 改为项目的连接字符串；</P>

<P>2、本文件夹内的所有.tt文件和.ttinclude文件复制到一个项目中；</P>

<P>3、MulitDALModel.tt 和 MulitDALModelDirect.tt 都是生成DAL层的模板，两个文件二选一即可。<br />
   A) MulitDALModelDirect.tt 生成的文件直接可用。<br />
     SQL语句的参数部分如下所示：<br />
       SqlParameter[] parameters = {<br />
								     new SqlParameter("@StudentClassName", classInfo.StudentClassName)<br />
                                   };</P>

  <P> B) MulitDALModel.tt 生成的文件中SqlDbType的类型为C#数据类型，需要手工更改为SQL Server数据类型。<br />
     SQL语句的参数部分如下所示，其中的 SqlDbType.String 应该更改为 SqlDbType.VarChar：<br />
        SqlParameter[] parameters = {<br />
										new SqlParameter("@StudentClassName", SqlDbType.String, 50)<br />
                                     };<br />
		parameters[0].Value = classInfo.StudentClassName;</P><br />

<P>4、依次打开其他所有的.tt文件并保存一次；</P>

<P>5、将产生的.cs文件（与.tt同名的.cs为空文件，不需要）复制到各项目中去（DBHelper.cs 的名字空间为 .DAL，默认位于DAL层中）；</P>


名字空间说明<br />
名字空间.Model :实体类<br />
名字空间.DAL:   数据访问层<br />
名字空间.BLL：  业务逻辑层<br />
