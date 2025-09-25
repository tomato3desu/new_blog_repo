---
title: nuxt × spring boot 
description: nuxt3 × spring bootでプロジェクトを作成する方法（開発用）
image: "images/springicon.jpg"
tags: ["nuxt", "spring boot"]
date: 2025-09-22
---

# nuxt3 × spring boot　開発用

nuxt.config.ts
```
export default defineNuxtConfig({
  compatibilityDate: '2025-09-19',
  devtools: { enabled: true },
  css: ['~/assets/css/main.css'],
  modules: ['@nuxt/image', '@nuxt/eslint', '@nuxtjs/tailwindcss'],
  runtimeConfig: {
    public: {
      apibase: 'http://localhost:8080'
    }
  }
})
```

config/Webconfig
```
package com.example.demo.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class Webconfig implements WebMvcConfigurer{
	
	@Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**") // 全てのエンドポイント対象
                        .allowedOrigins("http://localhost:3000","http://localhost:3001") // VueのURLを許可
                        .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                        .allowCredentials(true); // Cookieや認証情報も許可
            }
        };
    }
	
	@Override //画像公開
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/uploads/**")
                .addResourceLocations("file:" + System.getProperty("user.dir") + "/uploads/");
    }
}
```

エンドポイントを用意
```
package com.example.demo.controller;

import java.util.List;

import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.dto.StudentDto;
import com.example.demo.form.StudentForm;
import com.example.demo.service.StudentService;

import lombok.RequiredArgsConstructor;

@RestController
@RequiredArgsConstructor
public class StudentController {
	private final StudentService studentService;
	
	@GetMapping("/api/all")
	public List<StudentDto> getAll(){
		List<StudentDto> studentDtos = studentService.getAllStudent();
		
		return studentDtos;
	}
	
	@GetMapping("/api/student/{id}")
	public StudentDto getStudent(@PathVariable Long id) {
		StudentDto studentDto = studentService.getStudentById(id);
		
		return studentDto;
	}
	
	@PostMapping(value="/api/upload", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
	public void registerStudent(@ModelAttribute StudentForm form) {
		studentService.registerStudent(form);
	}
}

```

useFetchで取得
```
const config = useRuntimeConfig()
interface Student {
    id: number
    name: string
    grade: number
    image_path?: string
}

const { data: students } = await useFetch<Student[]>(`${config.public.apibase}/api/all`)
```