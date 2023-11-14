This repository is for exploring [RFdiffusion](https://github.com/RosettaCommons/RFdiffusion) work and my further protein design research topic.

## Unconditional monomer generation
Tell RFdiffusion that designs should be:

* 100-200 residues in length (randomly sampled each design) and 
* generate 10 such designs.

`python ../scripts/run_inference.py inference.output_prefix=example_outputs/design_unconditional 'contigmap.contigs=[100-200]' inference.num_designs=10`
![uncondtional_demo.gif](figure/unconditional.gif)

## Motif scaffolding (or inpainting)
Scaffolding site 5 from RSV-F protein (5TPN) and specify the protein we want to build, with the contig input:

* 10-40 residues (randomly sampled)
* residues 163-181 (inclusive) on the A chain of the input
* 10-40 residues (randomly sampled)
* generate 10 designs

`python ../scripts/run_inference.py inference.output_prefix=example_outputs/design_motifscaffolding inference.input_pdb=input_pdbs/5TPN.pdb 'contigmap.contigs=[10-40/A163-181/10-40]' inference.num_designs=10`
![motif_scaffolding_demo.gif](figure/motif_scaffolding.gif)

## Binder design
Designing binders to insulin receptor, without specifying the topology of the binder a prior. Describe the protein with the contig input:

* residues 1-150 of the A chain of the target protein
* a chainbreak (as we don't want the binder fused to the target!)
* A 70-100 residue binder to be diffused (the exact length is sampled each iteration of diffusion)
* Tell diffusion to target three specific residues on the target, specifically residues 59, 83 and 91 of the A chain
* generate 10 designs

`python ../scripts/run_inference.py inference.output_prefix=example_outputs/design_ppi inference.input_pdb=input_pdbs/insulin_target.pdb 'contigmap.contigs=[A1-150/0 70-100]' 'ppi.hotspot_res=[A59,A83,A91]' inference.num_designs=10 denoiser.noise_scale_ca=0 denoiser.noise_scale_frame=0`
![binder_design_demo.gif](figure/design_ppi.gif)