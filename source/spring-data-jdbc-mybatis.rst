#######################################
spring data jdbc 整合 mybatis
#######################################

CREATE DATABASE IF NOT EXISTS user_db_test;DROP TABLE IF EXISTS t_user;CREATE TABLE `t_user` (  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '用户id',  `username` varchar(64) NOT NULL COMMENT '用户姓名',  `age` int(11) NOT NULL COMMENT '用户年龄',  `mobile` varchar(11) DEFAULT NULL COMMENT '手机号',  PRIMARY KEY (`id`) USING BTREE) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;