# stage-2--third-sprint
第二阶段第三次总结：分别对登录和注册两个java文件进行一些java代码的编写，写一部分容错的内容，代码如下，注册部分：if((username == null||username.equalsIgnoreCase("")) || 
						(password == null||password.equalsIgnoreCase("")) 
						|| (conPassword == null||conPassword.equalsIgnoreCase(""))){
					Toast.makeText(ZhuCe.this, "用户名和密码是必填项",
							Toast.LENGTH_SHORT).show();
				}
				else{
					Cursor cursor=mDbHelper.getDiary(username);
					if(cursor.moveToFirst()){
						Toast.makeText(ZhuCe.this, "用户名已经存在",
								Toast.LENGTH_SHORT).show();
					}
					else if(!password.equals(conPassword)){
						Toast.makeText(ZhuCe.this, "两次密码输入不一致，请重新输入.",
								Toast.LENGTH_SHORT).show();
					}
					else{
						mDbHelper.createUser(username, password);
						Toast.makeText(ZhuCe.this, "注册成功，正转到登录界面，请稍后",
								Toast.LENGTH_SHORT).show();
						Intent intent3 = new Intent();
						intent3.setClass(ZhuCe.this, DengLu.class);
						startActivity(intent3);

					}

登录部分：if((nameString==null || nameString.equalsIgnoreCase(""))  || (passwordString==null || passwordString.equalsIgnoreCase("")))
				{
					Toast.makeText(DengLu.this, "用户名和密码是必填项", 1).show();
				}
				else{
					Cursor cursor=mDbHelper.getDiary(nameString);
					if(!cursor.moveToFirst())
					{
						Toast.makeText(DengLu.this, "该用户名不存在", 1).show();	
					}
					else if(!passwordString.equals(cursor.getString(2))){
						Toast.makeText(DengLu.this, "密码错误，请重新输入", 1).show();
					}
					else{
						if(cb.isChecked()){
							sp.edit().putString(nameString, passwordString).commit();
						}
						Toast.makeText(DengLu.this, "正在登录，请稍后...",
								Toast.LENGTH_SHORT).show();
		                Intent intent=new Intent(DengLu.this,MainExplain.class);
		                intent.putExtra("username", nameString);
		                finish();
		                startActivity(intent);
		                
					}
