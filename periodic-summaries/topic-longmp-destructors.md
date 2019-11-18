## Question

Should we make `longjmp` over frames with destructors undefined?

## Considerations

* Behavior is different across platforms
  * [MSVC]: 
    > If you use an /EH option to compile C++ code, destructors for local objects
    > are called during the stack unwind. However, if you use /EHs or /EHsc to
    > compile, and one of your functions that uses noexcept calls longjmp, then
    > the destructor unwind for that function might not occur, depending on the
    > optimizer state.
  * Other platforms: destructors are not called
* There are already cases in Rust where destructors are not called (e.g.
  `mem::forget`) that are not `unsafe`

## Conclusion

TBD

[zulip]: https://rust-lang.zulipchat.com/#narrow/stream/210922-wg-ffi-unwind/topic/longjmp.20interaction.20with.20destructors/
[MSVC]: https://docs.microsoft.com/en-us/cpp/cpp/using-setjmp-longjmp?view=vs-2019
