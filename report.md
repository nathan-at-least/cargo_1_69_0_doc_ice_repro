I triggered an ICE while running `cargo doc`.

I have pushed the reproduction repo to [cargo_1_69_0_doc_ice_repro](https://github.com/nathan-at-least/cargo_1_69_0_doc_ice_repro).

I am using cargo stable:

```
$ cargo --version
cargo 1.69.0 (6e9a83356 2023-04-12)
```

Here's the crashing command output:

```
$ cargo doc
 Documenting rustix v0.36.9
thread 'rustc' panicked at 'no resolutions for a doc link', compiler/rustc_metadata/src/rmeta/encoder.rs:2228:18
stack backtrace:
   0:     0x7c7d9119431a - std::backtrace_rs::backtrace::libunwind::trace::ha9053a9a07ca49cb
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/../../backtrace/src/backtrace/libunwind.rs:93:5
   1:     0x7c7d9119431a - std::backtrace_rs::backtrace::trace_unsynchronized::h9c2852a457ad564e
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/../../backtrace/src/backtrace/mod.rs:66:5
   2:     0x7c7d9119431a - std::sys_common::backtrace::_print_fmt::h457936fbfaa0070f
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys_common/backtrace.rs:65:5
   3:     0x7c7d9119431a - <std::sys_common::backtrace::_print::DisplayBacktrace as core::fmt::Display>::fmt::h5779d7bf7f70cb0c
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys_common/backtrace.rs:44:22
   4:     0x7c7d911f7b6e - core::fmt::write::h5a4baaff1bcd3eb5
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/core/src/fmt/mod.rs:1232:17
   5:     0x7c7d911872c5 - std::io::Write::write_fmt::h4bc1f301cb9e9cce
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/io/mod.rs:1684:15
   6:     0x7c7d911940e5 - std::sys_common::backtrace::_print::h5fcdc36060f177e8
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys_common/backtrace.rs:47:5
   7:     0x7c7d911940e5 - std::sys_common::backtrace::print::h54ca9458b876c8bf
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys_common/backtrace.rs:34:9
   8:     0x7c7d91196e5f - std::panicking::default_hook::{{closure}}::hbe471161c7664ed6
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/panicking.rs:271:22
   9:     0x7c7d91196b9b - std::panicking::default_hook::ha3500da57aa4ac4f
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/panicking.rs:290:9
  10:     0x7c7d943f88b5 - <rustc_driver_impl[fb92b3e21ac03dce]::DEFAULT_HOOK::{closure#0}::{closure#0} as core[911a585bea10363d]::ops::function::FnOnce<(&core[911a585bea10363d]::panic::panic_info::PanicInfo,)>>::call_once::{shim:vtable#0}
  11:     0x7c7d9119769d - <alloc::boxed::Box<F,A> as core::ops::function::Fn<Args>>::call::h6507bddc3eebb4a5
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/alloc/src/boxed.rs:2001:9
  12:     0x7c7d9119769d - std::panicking::rust_panic_with_hook::h50c09d000dc561d2
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/panicking.rs:696:13
  13:     0x7c7d91197419 - std::panicking::begin_panic_handler::{{closure}}::h9e2b2176e00e0d9c
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/panicking.rs:583:13
  14:     0x7c7d91194786 - std::sys_common::backtrace::__rust_end_short_backtrace::h5739b8e512c09d02
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys_common/backtrace.rs:150:18
  15:     0x7c7d91197122 - rust_begin_unwind
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/panicking.rs:579:5
  16:     0x7c7d911f3ec3 - core::panicking::panic_fmt::hf33a1475b4dc5c3e
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/core/src/panicking.rs:64:14
  17:     0x7c7d911f4031 - core::panicking::panic_display::ha103dd28e5023b08
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/core/src/panicking.rs:147:5
  18:     0x7c7d911f3fdb - core::panicking::panic_str::h940bf021f492dc8c
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/core/src/panicking.rs:131:5
  19:     0x7c7d911f3c46 - core::option::expect_failed::h09b982639336e7ea
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/core/src/option.rs:2045:5
  20:     0x7c7d948c3b77 - <rustc_metadata[29cf5a64f33334d8]::rmeta::encoder::provide::{closure#0} as core[911a585bea10363d]::ops::function::FnOnce<(rustc_middle[1a4ce3311a146f18]::ty::context::TyCtxt, rustc_span[fab0eb11f1fed58d]::def_id::DefId)>>::call_once
  21:     0x7c7d94ccc3ad - rustc_query_system[caf472e4bac2b2b6]::query::plumbing::try_execute_query::<rustc_query_impl[a4bd04fc7a0236b8]::queries::doc_link_resolutions, rustc_query_impl[a4bd04fc7a0236b8]::plumbing::QueryCtxt>
  22:     0x7c7d94d4d7cd - <rustc_query_impl[a4bd04fc7a0236b8]::Queries as rustc_middle[1a4ce3311a146f18]::ty::query::QueryEngine>::doc_link_resolutions
  23:     0x5adfda56f498 - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector>::resolve_path
  24:     0x5adfda56f74e - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector>::resolve
  25:     0x5adfda573364 - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector as rustdoc[483c6e22976f34cb]::visit::DocVisitor>::visit_item
  26:     0x5adfda57c67a - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector as rustdoc[483c6e22976f34cb]::visit::DocVisitor>::visit_inner_recur
  27:     0x5adfda576a7c - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector as rustdoc[483c6e22976f34cb]::visit::DocVisitor>::visit_item
  28:     0x5adfda57c67a - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector as rustdoc[483c6e22976f34cb]::visit::DocVisitor>::visit_inner_recur
  29:     0x5adfda576a7c - <rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::LinkCollector as rustdoc[483c6e22976f34cb]::visit::DocVisitor>::visit_item
  30:     0x5adfda56e0a2 - rustdoc[483c6e22976f34cb]::passes::collect_intra_doc_links::collect_intra_doc_links
  31:     0x5adfda4b632e - <rustc_session[b87ece769e9b9511]::session::Session>::time::<rustdoc[483c6e22976f34cb]::clean::types::Crate, rustdoc[483c6e22976f34cb]::core::run_global_ctxt::{closure#7}>
  32:     0x5adfda5e1dd0 - rustdoc[483c6e22976f34cb]::core::run_global_ctxt
  33:     0x5adfda4b65b9 - <rustc_session[b87ece769e9b9511]::session::Session>::time::<(rustdoc[483c6e22976f34cb]::clean::types::Crate, rustdoc[483c6e22976f34cb]::config::RenderOptions, rustdoc[483c6e22976f34cb]::formats::cache::Cache), rustdoc[483c6e22976f34cb]::main_args::{closure#1}::{closure#0}::{closure#0}::{closure#0}>
  34:     0x5adfda3b4d57 - <rustc_middle[1a4ce3311a146f18]::ty::context::GlobalCtxt>::enter::<rustdoc[483c6e22976f34cb]::main_args::{closure#1}::{closure#0}::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>
  35:     0x5adfda41ffce - rustc_span[fab0eb11f1fed58d]::with_source_map::<core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>, rustc_interface[bd8390756bd7a52a]::interface::run_compiler<core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>, rustdoc[483c6e22976f34cb]::main_args::{closure#1}>::{closure#0}::{closure#0}>
  36:     0x5adfda392474 - <scoped_tls[473f62cd2eff9842]::ScopedKey<rustc_span[fab0eb11f1fed58d]::SessionGlobals>>::set::<rustc_interface[bd8390756bd7a52a]::interface::run_compiler<core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>, rustdoc[483c6e22976f34cb]::main_args::{closure#1}>::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>
  37:     0x5adfda4cd9a0 - std[685882fd5f6d52e5]::sys_common::backtrace::__rust_begin_short_backtrace::<rustc_interface[bd8390756bd7a52a]::util::run_in_thread_pool_with_globals<rustc_interface[bd8390756bd7a52a]::interface::run_compiler<core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>, rustdoc[483c6e22976f34cb]::main_args::{closure#1}>::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>::{closure#0}::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>
  38:     0x5adfda5981dd - <<std[685882fd5f6d52e5]::thread::Builder>::spawn_unchecked_<rustc_interface[bd8390756bd7a52a]::util::run_in_thread_pool_with_globals<rustc_interface[bd8390756bd7a52a]::interface::run_compiler<core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>, rustdoc[483c6e22976f34cb]::main_args::{closure#1}>::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>::{closure#0}::{closure#0}, core[911a585bea10363d]::result::Result<(), rustc_span[fab0eb11f1fed58d]::ErrorGuaranteed>>::{closure#1} as core[911a585bea10363d]::ops::function::FnOnce<()>>::call_once::{shim:vtable#0}
  39:     0x7c7d911a1593 - <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once::h39990b24eedef2ab
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/alloc/src/boxed.rs:1987:9
  40:     0x7c7d911a1593 - <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once::h01a027258444143b
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/alloc/src/boxed.rs:1987:9
  41:     0x7c7d911a1593 - std::sys::unix::thread::Thread::new::thread_start::ha4f1cdd9c25884ba
                               at /rustc/84c898d65adf2f39a5a98507f1fe0ce10a2b8dbc/library/std/src/sys/unix/thread.rs:108:17
  42:     0x7c7d9103dea7 - start_thread
  43:     0x7c7d90f5da2f - clone
  44:                0x0 - <unknown>

error: the compiler unexpectedly panicked. this is a bug.

note: we would appreciate a bug report: https://github.com/rust-lang/rust/issues/new?labels=C-bug%2C+I-ICE%2C+T-compiler&template=ice.md

note: rustc 1.69.0 (84c898d65 2023-04-16) running on x86_64-unknown-linux-gnu

note: compiler flags: --crate-type lib

note: some of the compiler flags provided by cargo are hidden

query stack during panic:
#0 [doc_link_resolutions] resolutions for documentation links for a module
end of query stack
error: could not document `rustix`

Caused by:
  process didn't exit successfully: `rustdoc --edition=2018 --crate-type lib --crate-name rustix /home/user/.cargo/registry/src/github.com-1ecc6299db9ec823/rustix-0.36.9/src/lib.rs --cap-lints allow -o /home/user/hack/rust-doc-ice-2023-04-25/target/doc --cfg 'feature="default"' --cfg 'feature="io-lifetimes"' --cfg 'feature="libc"' --cfg 'feature="std"' --cfg 'feature="termios"' --cfg 'feature="use-libc-auxv"' --error-format=json --json=diagnostic-rendered-ansi,artifacts,future-incompat --diagnostic-width=194 -C metadata=68c48281f8d51e01 -L dependency=/home/user/hack/rust-doc-ice-2023-04-25/target/debug/deps --extern bitflags=/home/user/hack/rust-doc-ice-2023-04-25/target/debug/deps/libbitflags-1a1c34f79f6e612c.rmeta --extern io_lifetimes=/home/user/hack/rust-doc-ice-2023-04-25/target/debug/deps/libio_lifetimes-cd6be4f8fe3b4bc6.rmeta --extern libc=/home/user/hack/rust-doc-ice-2023-04-25/target/debug/deps/liblibc-25f8caa1cd741fae.rmeta --extern linux_raw_sys=/home/user/hack/rust-doc-ice-2023-04-25/target/debug/deps/liblinux_raw_sys-a98848148f479f38.rmeta --crate-version 0.36.9 --cfg linux_raw` (exit status: 101)
```
