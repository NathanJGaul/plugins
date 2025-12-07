---
description: Use this skill as a base profile for systems programming courses in C, C++, Rust, or Zig. Provides core concepts for memory management, performance awareness, safety considerations, and low-level understanding. Language-specific profiles inherit from this. Trigger when user mentions "systems programming", "low-level programming", or "performance-critical development".
---

# Systems Programming - Base Course Profile

**Category:** Low-level programming, memory management, performance-critical development
**Applicable Languages:** C, C++, Rust, Zig

## Overview

This is a base profile for systems programming courses. Language-specific profiles (like C++ Fundamentals) inherit from this and customize for their specific language and audience.

## Core Concepts (All Systems Languages)

### Memory Management
- Stack vs heap allocation
- Object lifetime and ownership
- Memory layout and alignment
- Manual vs automatic memory management

### Performance Awareness
- Understanding what code compiles to
- Cache-friendly data structures
- Avoiding unnecessary copies
- Profiling and optimization

### Safety Considerations
- Buffer overflows and bounds checking
- Use-after-free and dangling references
- Data races and thread safety
- Undefined behavior awareness

### Low-Level Understanding
- How the CPU executes code
- System calls and OS interaction
- File I/O at the system level
- Network programming basics

## Pedagogical Approach

### Visualization is Critical
Systems programming deals with invisible concepts. Make them visible:
- Memory layout diagrams for every pointer topic
- Stack frame illustrations
- Heap allocation visualizations
- Data structure memory representations

### Compile-Time vs Runtime
Help students distinguish:
- What the compiler does vs what happens at runtime
- Static vs dynamic properties
- Compile-time errors vs runtime errors

### Error-Driven Learning
Compiler errors and crashes are learning tools:
- Show what broken code looks like
- Teach students to read error messages
- Build pattern recognition for common issues

## Framework-Free Teaching

Systems programming courses should typically:
- Focus on standard library only
- Build fundamental understanding first
- Avoid abstractions that hide important details
- Let students feel the "weight" of manual management

## Lab Structure

### Environment Requirements
- Must compile and run locally (not just online)
- Debugger access is essential
- Students need to see memory state

### Challenge Design
- Start with working code to modify
- Include "break this code" exercises
- Require debugging exercises
- Test with edge cases and invalid input

## Assessment Considerations

### Compilation is Non-Negotiable
- Code that doesn't compile fails
- Partial credit for compiling code with bugs
- Full error messages must be understood

### Memory Safety Checks
- Use sanitizers (ASan, MSan, UBSan) in testing
- Valgrind for memory leak detection
- Points deducted for memory errors

### Performance Requirements (When Applicable)
- Specify complexity requirements
- Test with large inputs
- Compare against reference implementation
