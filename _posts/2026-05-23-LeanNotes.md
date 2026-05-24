---
layout:     post
title:      LeanNotes
subtitle:   
date:       2026-05-23
author:     Zachary Wang
header-img: img/Post_bg.jpg
catalog: true
tags:
    - Notes
---

## 被 ai agent 搞破防了

感觉自己会一些 lean grammar 还是很有必要的. 本篇暂时以问题形式记录.

### Repr 的作用是什么?

打印 structure 的内容

### BEq 的作用是什么?

赋予**判断**两个同类型的 var 是否相等的能力

### DecidableEq 的作用是什么?

赋予**证明**两个同类型的 var 相等或者不等的能力

### inductive 和 structure 的区别?

structure EnumAtom where 
  | name : String
  | deriving Repr, BEq, DecidableEq

会自动生成 constructor 和访问器

EnumAtom.mk : String → EnumAtom
EnumAtom.name : EnumAtom → String

structure 会自动为新定义的类型设置构造子。更具体的例子就是：

structure Person where
  | name : String
  | age : Int

表示一个人有两种属性。而

inductive Color where
  | red
  | green
  | blue

表示一个 Color 中包含三种可能的颜色。

### 含参数的 inductive（类型构造器）

inductive Box (α : Type) where
  | mk : α → Box α

这里 Box : Type → Type, 即把一个类型映射到另一个类型。

### LE 是一个类型类（Type Class）是什么意思?

instance : LE IdxAtom where
  le a b := match a, b with
    | IdxAtom.int m, IdxAtom.int n => m ≤ n
    | IdxAtom.int _, IdxAtom.enumatom _ => true
    | IdxAtom.enumatom _, IdxAtom.int _ => false
    | IdxAtom.enumatom e₁, IdxAtom.enumatom e₂ => e₁.name ≤ e₂.name

LE 是一个为 type 打的标签, 这个 instance 表示 type IdxAtom 中的 var 可以建立 LE 关系, 下面给出的是具体的建立这种关系应该遵循的规则.

###  isTrue 和 True 有什么区别?

isTrue 可以理解成带证明的判断.

### 有下划线表示这个变量是 unsed 的

--   ⟦c⟧ᴱ(ρ) = ok(c)
--   ⟦n⟧ᴱ(ρ) = ok(n)
--   ⟦r⟧ᴱ(ρ) = ok(r)
--   ⟦x⟧ᴱ(ρ) = ok(ρ(x))  if x ∈ dom(ρ)
--             err(UnboundId(x)) otherwise

/-- Evaluation function for expressions: ⟦e⟧ᴱ : Env → EvalResult -/
def evalExpr : Expr → Env → EvalResult
  | Expr.mc (Mznc.bool b), _ρ => EvalResult.ok (Val.bool b)
  | Expr.mc (Mznc.enum e), _ρ => EvalResult.ok (Val.enumatom e)
  | Expr.Mznint n, _ρ => EvalResult.ok (Val.int n)
  | Expr.Mznfloat f, _ρ => EvalResult.ok (Val.float f)
  | Expr.MznVar x, ρ => EvalResult.ok (ρ x)
  | _, _ => EvalResult.ok (Val.bool true)  -- placeholder for other expressions

### 