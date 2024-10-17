# @Valid, addFlashAttribute, addAttribute를 함께 사용하는 이유

`@Valid`, `addFlashAttribute`, `addAttribute`를 함께 사용하는 주요 이유는 폼 제출 처리와 관련된 유효성 검사, 메시지 전달, 그리고 데이터 전송을 효과적으로 수행하기 위해서입니다.

#### 유효성 검사와 메시지 전달

##### 1. 데이터 유효성 검증

- `@Valid` 어노테이션은 폼에서 제출된 데이터의 유효성을 자동으로 검사합니다.

##### 2. 오류 메시지 전달

- 유효성 검사 실패 시, `addFlashAttribute`를 사용하여 오류 메시지를 일회성으로 전달할 수 있습니다.

##### 3. 성공 메시지 전달

- 유효성 검사 성공 시, `addFlashAttribute`를 통해 성공 메시지를 전달할 수 있습니다.

##### 4. 지속적인 데이터 전달

- `addAttribute`를 사용하여 URL 파라미터로 데이터를 전달하면 값이 유지됩니다.

#### 장점

- **보안성 향상:** `addFlashAttribute`는 URL에 데이터를 노출하지 않아 중요한 정보를 안전하게 전달할 수 있습니다.
- **일회성 데이터 전달:** `addFlashAttribute`로 전달된 메시지는 한 번만 표시되고 사라지므로, 페이지 새로고침 시 중복 표시를 방지합니다.
- **사용자 경험 개선:** 유효성 검사 결과와 관련 메시지를 즉시 사용자에게 보여줄 수 있습니다.
- **데이터 지속성 선택:** `addAttribute`를 사용하면 URL에 데이터가 포함되어 지속적으로 사용 가능합니다.

#### 사용 예시

```java
@PostMapping("/submit")
public String submitForm(@Valid @ModelAttribute("formData") FormData formData, 
                         BindingResult result, 
                         RedirectAttributes redirectAttributes) {
    if (result.hasErrors()) {
        redirectAttributes.addFlashAttribute("errors", result.getAllErrors());
        return "redirect:/form";
    }
    
    // 폼 처리 로직
    redirectAttributes.addAttribute("id", formData.getId());
    redirectAttributes.addFlashAttribute("message", "Form submitted successfully");
    
    return "redirect:/success";
}
```

- `@Valid`는 `FormData` 객체의 유효성을 검사하고, `addFlashAttribute`는 오류 또는 성공 메시지를 일회성으로 전달하며, `addAttribute`는 id를 URL 파라미터로 전달합니다.

- 이 방식은 폼 처리 후 리다이렉트 시 유용한 피드백을 제공하면서도 필요한 데이터를 적절히 전달할 수 있는 효과적인 방법입니다.
