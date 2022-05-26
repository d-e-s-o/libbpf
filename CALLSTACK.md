bpf_object__load
-> bpf_object_load
  -> bpf_object__resolve_externs
  -> bpf_object__resolve_ksyms_btf_id
    -> (bpf_object__resolve_ksym_var_btf_id | bpf_object__resolve_ksym_func_btf_id)
    -> bpf_core_types_are_compat
  -> bpf_object__relocate
    -> bpf_object__relocate_core
      -> bpf_core_resolve_relo
        -> bpf_core_find_cands
        -> bpf_core_calc_relo_insn
          -> bpf_core_parse_spec // does nothing for type base relocations
          for each candiate:
            -> bpf_core_spec_match
              if type base relocation:
              -> bpf_core_types_are_compat
          -> bpf_core_calc_relo
            if type based relocation:
            -> bpf_core_calc_type_relo
              - just sets bpf_core_relo_res->{old_val,new_val} to 1??

      -> bpf_core_patch_insn
        - uses bpf_core_relo_res->{old_val,new_val}, depending on
          instruction type
